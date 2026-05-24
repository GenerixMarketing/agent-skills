# Versions

Changelog for agent-skills. Follows [semantic versioning](https://semver.org/) loosely: major versions for breaking changes (skill renames, removed skills), minor for new skills, patch for fixes and clarifications.

## Unreleased

Next: AEO category (answer engine optimization). Likely first skills: aeo-foundations, citation-tracking, content-for-citations.

## v0.5.0 (2026-05-23)

SEO category complete with this release. Eight SEO skills now shipped covering primer, on-page, technical, keyword, competitor, off-page, content portfolio, and local search.

- Added `seo/off-page-link-building` skill: white-hat authority and link strategy covering digital PR, expert sourcing, local citations, partner backlinks, content-earned links, and reclamation. Explicitly refuses link schemes, PBNs, paid networks, and other tactics that risk manual actions. Includes link quality rubric, outreach templates, foundational citation source list, and a worked example.
- Added `seo/content-audit` skill: portfolio-level inventory and prune workstream. Classifies every URL as keep, improve, consolidate, prune, or redirect. Especially valuable for sites affected by helpful content algorithm updates. Includes classification rubric, HCU recovery playbook, and a worked example.
- Added `seo/local-seo` skill: balanced strategy across Google Business Profile (local pack play) and on-site local SEO (organic blue-link play). Includes GBP optimization checklist, reviews program playbook, local schema templates for common business types, and a worked example.
- Updated Skills Index to mark SEO category complete with all eight skills shipped.

## v0.4.0 (2026-05-23)

- Added `seo/keyword-research` skill: tool-agnostic workflow with adapter sections for Semrush MCP, Ahrefs, GSC, Google Keyword Planner, and free fallbacks. Includes intent classification reference, scoring framework, SERP feature guide, and a worked example for the fictional Cardinal Ridge Roofing.
- Added `seo/competitor-analysis` skill: three-tier competitor framing (direct, aspirational, shadow) with extended treatment of shadow competitors (Reddit, YouTube, AI Overviews, review sites). Includes shadow competitor playbook, content gap method reference, and a worked example.
- Updated Skills Index to show keyword-research and competitor-analysis as Shipped.

## v0.3.0 (2026-05-23)

- Added `seo/seo-foundations` skill: SKILL.md and a quotable glossary reference. Acts as the conceptual primer the rest of the SEO category builds on.
- Added `seo/on-page-audit` skill: SKILL.md, ten-point checklist, title and meta description pattern library, and a worked audit example on a fictional service page.
- Added `seo/technical-audit` skill: SKILL.md, crawl-setup reference (Screaming Frog and free alternatives), GSC pulls reference, dev-ticket templates for the ten most common findings, and a worked audit example on a fictional mid-size site.
- Updated Skills Index to show the three SEO foundations as Shipped, with planned SEO skills listed separately.

## v0.2.0 (2026-05-22)

- Added `_foundation/client-context` skill: SKILL.md, intake-questions reference, and a worked example for a sample SMB client
- Added Quick Start section to README covering install paths, the recommended first prompt, and the role of the foundation skill
- Updated Skills Index to show `client-context` as Shipped

## v0.1.1 (2026-05-20)

- Migrated repo from `GenerixMarketing/agent-skills` user account to `Generix-Marketing/agent-skills` organization
- Updated internal links to reference the new org URL
- Old URL continues to redirect to the new location

## v0.1.0 (2026-05-19)

Initial repo setup.

- Added `README.md` with category overview and usage instructions
- Added `CLAUDE.md` with Claude Code-specific conventions
- Added `AGENTS.md` for cross-agent compatibility (Cursor, Windsurf, Codex)
- Added `CONTRIBUTING.md` with skill submission guidelines
- Added `LICENSE` (MIT)
- Added `.gitignore`
- Added `validate-skills.sh` for SKILL.md frontmatter validation
- Established planned structure for 32 skills across SEO, AEO, Content, and Analytics categories
