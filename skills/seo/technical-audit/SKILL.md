---
name: technical-audit
description: Use this skill when the user asks for a site-wide technical SEO audit, wants to crawl their site, asks about indexation issues across multiple URLs, mentions Core Web Vitals or page speed across a site, asks about redirect chains, broken links, sitemap problems, robots.txt issues, duplicate content, or orphan pages. Triggers include "audit my site," "crawl my site," "why are pages not getting indexed," "find broken links," "check my sitemap," "site-wide SEO review," "technical SEO." This skill coordinates a crawl (Screaming Frog, Sitebulb, or a free alternative) and a Google Search Console pull, then identifies site-wide issues and prioritizes the work. Reads client-context.md if present. Use on-page-audit for single-page audits.
---

# Technical Audit

This skill runs a site-wide technical SEO audit. It coordinates a crawl, pulls Google Search Console data, and produces a prioritized report of issues across the whole site. The output is a deliverable the user can hand to a developer with specific tickets to file.

## When to Run This Skill

Run it when:

- The user asks for a site-wide audit, technical audit, or "full SEO review"
- The user mentions indexation problems across multiple pages
- The user is onboarding a new client and needs a baseline
- The user is investigating a traffic drop and needs to rule out technical causes
- The user is post-migration (replatform, domain change, redesign) and needs to catch regressions

Skip it when:

- The user wants a single-page audit (use `on-page-audit`)
- The user wants help picking keywords (use `keyword-research`)
- The user is asking conceptual questions (use `seo-foundations`)
- The site is under 50 pages and the user really just wants on-page audits of the main URLs

## Before You Start

### 1. Read client-context.md

If `client-context.md` exists in the working directory, read it. The audit's recommendations get sharper when you know the CMS (some fixes have CMS-specific paths), the dev resources available (some recommendations are off the table without a developer), and the goals (a lead-gen site has different priorities than an ecommerce site).

If it does not exist, proceed but note in the report that recommendations are generic.

### 2. Decide what tools you have access to

Check what is available in this order:

1. **Live crawl tools.** Does the user have Screaming Frog installed? Sitebulb? Ahrefs Site Audit? Semrush Site Audit? If yes, ask them to run the crawl and share the export. These give the deepest picture.
2. **Free crawl alternative.** No paid tool? Run a crawl using a Python script with `requests` and `BeautifulSoup`, or use a free online crawler. Coverage is shallower but workable for sites under 1,000 pages.
3. **Search Console MCP.** If the user has `mcp__8f9a1ad3-1f56-4b63-9801-55f7b6a76dc5__gsc-*` tools available, pull indexation data, performance data, and coverage reports directly.
4. **Browser inspection.** Use Claude in Chrome for sampled page inspection (key templates, the homepage, top traffic pages).

You do not need every tool to produce value. Document what you used and what you did not have access to. Flag the gaps in the report.

### 3. Define the scope

Ask: "Are we auditing the full site, or a specific section?" For sites over 5,000 URLs, narrow the scope first. A focused audit on the blog or the product catalog is more useful than a shallow audit on everything.

## The Audit (Twelve Areas, Prioritized)

Walk through these in order. The order goes from "shows up in Search Console as red" to "would be nice to clean up."

### 1. Indexation Health

- Pull the GSC Coverage report (or Pages report in modern GSC).
- How many URLs are Indexed?
- How many are Indexed but not submitted in sitemap (often shows orphans or unintended exposure)?
- How many are Submitted in sitemap but not indexed (often the most actionable group)?
- How many are Excluded? Group by reason: noindex, canonicalized, duplicate, crawled but not indexed, discovered but not indexed.
- For Excluded, Crawled but not indexed: this is usually a content quality signal. Sample 5-10 URLs and assess.
- For Excluded, Discovered but not indexed: Google found them but did not crawl. Usually a crawl budget or quality signal. Common on large or thin sites.

### 2. Crawlability

- Fetch `robots.txt`. Confirm it does not block important URLs by accident. Common mistakes: blocking `/wp-admin/` is fine, blocking `/wp-content/` breaks image and CSS rendering.
- Fetch the XML sitemap(s). Are they returning 200? Are URLs in the sitemap actually indexable (not noindexed, not redirected, not 404)?
- Check the sitemap is referenced in robots.txt.
- Are there orphaned URLs (in the sitemap but with zero internal links pointing to them)? Use the crawl to identify.
- Are there URLs with no internal links and not in the sitemap (true orphans)? These will not be discovered.

### 3. Status Codes and Redirects

From the crawl export:

- How many URLs return 4xx? Group by template if possible. A handful of 404s is fine; hundreds suggest a broken nav or a deleted section that still has links.
- How many URLs return 5xx? Even one should be investigated.
- How many redirect chains exist (A → B → C or longer)? Collapse to A → C.
- How many 302s exist where 301s should be? Convert.
- Are there mixed-case duplicate URLs (both `/About-Us` and `/about-us` returning 200)? Pick one, 301 the other.
- Are there trailing-slash duplicates (`/page` and `/page/` both returning 200)? Pick one canonical pattern.

### 4. Canonicalization

- Are canonical tags present on every page?
- Are any canonicals pointing to non-200 URLs (canonical to a 301 or 404)?
- Are any canonicals self-conflicting (page X canonicals to page Y, page Y canonicals to page X)?
- Are paginated archives canonicalized correctly? Each page should self-canonical, not all canonical to page 1 (Google deprecated rel=next/prev guidance but the behavior still matters).

### 5. Duplicate Content

- Are there pages with identical or near-identical content?
- Common offenders: faceted navigation on ecommerce (`?color=red&size=large`), printer-friendly versions, tag and category archives, location pages with templated content and only the city name swapped.
- For each duplicate cluster, pick one canonical URL and either canonical the others or noindex them.

### 6. Internal Linking and Site Structure

- What is the average click depth from the homepage? Pages 4+ clicks deep usually underperform.
- Which pages have zero internal links pointing to them?
- Are there pages with hundreds of incoming internal links that should not have them (boilerplate footer links pointing to "About" from every page is fine; same volume pointing to a buried blog post is wasted equity)?
- Is the navigation logical? Can a user (and a crawler) reach the most important pages from the homepage in two clicks?

### 7. Mobile Rendering and Mobile-First Indexing

- Sample 5-10 pages across templates (homepage, service page, blog post, product page, landing page).
- Does the mobile version of each page render correctly?
- Are critical content and CTAs present in the mobile version (not stripped for mobile)?
- Are tap targets large enough?
- Is there content above the fold on mobile, or just a hero image?

### 8. Core Web Vitals

- Pull Core Web Vitals data from GSC (Page Experience report) or PageSpeed Insights.
- Group URLs by status: Good / Needs Improvement / Poor for each of LCP, INP, CLS.
- For each metric showing a Poor cluster, identify the template causing it (often a single template, the blog post template, or the product page template, is responsible for most of the failures).
- Lighthouse top opportunities, grouped by template.

### 9. Schema Markup

- What schema types are deployed and on which templates?
- Are required fields populated correctly?
- Run a sample of pages through the Rich Results Test.
- Are there opportunities for additional schema (FAQPage on FAQ sections, BreadcrumbList on every page, LocalBusiness on local landers, Product on product pages)?

### 10. International and Hreflang (If Applicable)

If the site is monolingual and single-region, skip this section.

If multi-language or multi-region:

- Are hreflang tags present on every page?
- Are hreflang tags symmetric (page A links to page B as alternate, page B links to page A as alternate)?
- Are the language and region codes valid (ISO 639-1 for language, ISO 3166-1 alpha-2 for region)?
- Is the `x-default` set for international audiences who do not match a specific locale?

### 11. Security and HTTPS

- Is the entire site on HTTPS? Any HTTP URLs returning 200 should be flagged.
- Is there mixed content (HTTPS pages loading HTTP assets)? Browser console will flag.
- Is HSTS enabled?
- Is the SSL certificate current?

### 12. Log File Analysis (If Available)

If the user can share server logs:

- Which URLs is Googlebot actually crawling?
- Is Googlebot wasting crawl budget on URLs that should not be indexed (parameter URLs, internal search results, admin paths)?
- Are there important URLs Googlebot never crawls?

This is the deepest signal available but most clients cannot share logs easily. Skip if not available; note in the report.

## Output Format

Always produce the report in this structure:

```markdown
# Technical SEO Audit: [Domain]

**Audit period:** [YYYY-MM-DD]
**Auditor:** [Agent or user]
**Scope:** [Full site / specific section / sample]
**Tools used:** [Screaming Frog v.X, GSC export YYYY-MM-DD, PageSpeed Insights, etc.]

## Executive Summary

[Three to five sentences. State of the site overall. Biggest issue. Estimated impact of fixes. Recommended sequencing.]

## Top Five Fixes (Do These First)

1. **[Fix name]**, [What is broken, what is the fix, who owns it, estimated impact.]
2. **[Fix name]**, [...]
3. **[Fix name]**, [...]
4. **[Fix name]**, [...]
5. **[Fix name]**, [...]

## Findings by Area

### 1. Indexation Health
[Numbers + interpretation + recommendations.]

### 2. Crawlability
[...]

### 3. Status Codes and Redirects
[...]

### 4. Canonicalization
[...]

### 5. Duplicate Content
[...]

### 6. Internal Linking and Site Structure
[...]

### 7. Mobile Rendering
[...]

### 8. Core Web Vitals
[...]

### 9. Schema Markup
[...]

### 10. International and Hreflang
[Or "N/A, single language, single region site."]

### 11. Security and HTTPS
[...]

### 12. Log File Analysis
[Or "Not available for this audit."]

## Issue Backlog (for Dev / SEO Team)

| Priority | Issue | Affected URLs | Effort | Owner | Linked Finding |
|---|---|---|---|---|---|
| P0 | [Issue title] | [Count or list] | [Hours / days] | Dev / SEO / Content | [§X above] |

## What This Audit Did Not Cover

[Be explicit about gaps: server logs not available, JavaScript-rendered content not fully crawled, specific subdomains excluded, etc. This protects the audit and tells the client what to add later.]

## Recommended Next Steps

1. [Highest priority action]
2. [Next action]
3. [Re-audit cadence: quarterly is standard.]
```

## How to Prioritize Fixes

Use four tiers:

- **P0, Stop the bleeding.** Indexation regressions, sitewide 5xx errors, broken canonicals on revenue pages, security warnings. Fix this week.
- **P1, Material impact.** Indexation issues affecting >10% of URLs, redirect chains on high-traffic pages, mobile rendering failures on key templates, Core Web Vitals failing on top traffic pages. Fix this sprint.
- **P2, Cleanup with measurable upside.** Duplicate content, orphan pages, schema additions on templates that would qualify for rich results, internal linking gaps. Fix this quarter.
- **P3, Hygiene.** Stale sitemap entries, single 404s with low traffic, minor schema warnings. Fix when convenient.

Anything at P0 or P1 goes into the Top Five Fixes section of the report. P2 and P3 live in the Issue Backlog table.

## Re-audit Cadence

Recommend quarterly. After the first audit, subsequent audits are faster because the baseline is known and the work is "diff against last audit." For sites under active development, monthly is better.

Always re-run after:

- A site migration (domain, platform, structure)
- A major redesign
- A traffic drop of more than 15% week over week
- A Google algorithm update flagged in the SEO community

## When the User Pushes Back

Two common pushbacks:

**"Do I really need a full audit?"** If they are asking, the answer is probably yes, but you can offer a fast first pass: indexation + status codes + sitemap, three areas, two hours of work. If that surfaces nothing, the full audit can wait.

**"I do not have access to a crawler."** Offer the free fallback (Python script crawl, or use the free tier of an online crawler like Screaming Frog free version up to 500 URLs). The audit will be shallower but useful. Document the limit in the report.

## Common Pitfalls

- **Drowning the client in a 50-page report.** The Top Five Fixes section is what they will read. Make sure it is correct, action-oriented, and owned. The rest of the report is reference material.
- **Recommending the wrong fix for the symptom.** "Pages excluded from index" can mean noindex, canonicalization, thin content, or duplicate content. Each has a different fix. Diagnose before prescribing.
- **Ignoring the CMS.** A WordPress site has different fix paths than a Shopify site than a custom build. Reference the CMS from `client-context.md` and write recommendations the team can actually implement.
- **Skipping the "what this audit did not cover" section.** This protects you and the client. If you did not have logs, say so. If you crawled a sample, say which URLs.
- **Treating Core Web Vitals as the most important finding.** It is rarely the biggest lever. A site with great CWV but a noindex on its main service page has bigger problems. Pull CWV up only if it is the bottleneck.

## References

- `references/crawl-setup.md`: How to configure Screaming Frog (and free alternatives) for an effective crawl, including which settings to change from defaults.
- `references/gsc-pulls.md`: The specific Search Console reports to pull, what each one tells you, and how to interpret the most common patterns.
- `references/issue-templates.md`: Pre-written ticket descriptions for the ten most common findings, ready to paste into Jira / Linear / Asana.
- `examples/sample-technical-audit.md`: A worked audit on a fictional mid-size site.
