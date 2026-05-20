# Contributing to agent-skills

Thanks for considering a contribution. This guide explains how to add a new skill, improve an existing one, or fix a bug.

## Before You Start

1. Check the [open issues](https://github.com/Generix-Marketing/agent-skills/issues) to see if your idea is already being worked on.
2. For new skills, open an issue first to discuss scope. Some categories may already have a planned skill that overlaps.
3. For typo fixes, small clarifications, or rule additions, just open a pull request.

## Adding a New Skill

### 1. Pick the right category

Skills belong in one of these folders:

- `skills/seo/`: Traditional SEO work
- `skills/aeo/`: AI citation and answer-engine optimization
- `skills/content/`: Content strategy, schema, site architecture
- `skills/analytics/`: Measurement and reporting

If your skill doesn't fit any of these, open an issue to discuss whether a new category makes sense or whether the skill belongs elsewhere.

### 2. Create the folder structure

```
skills/[category]/[skill-name]/
├── SKILL.md          # Required
├── references/       # Optional, for skill-specific reference docs
└── examples/         # Optional, for worked examples
```

Use kebab-case for folder names (`seo-technical`, not `seo_technical` or `SEOTechnical`).

### 3. Write SKILL.md

Every `SKILL.md` starts with YAML frontmatter:

```yaml
---
name: your-skill-name
description: When the user wants to [specific task]. Also use when the user mentions [trigger phrases or keywords]. Use this when [conditions].
---
```

The `description` field decides whether the agent loads your skill. Be specific. Vague descriptions cause the skill to load when it shouldn't, or fail to load when it should. Read existing skill descriptions for the pattern.

After the frontmatter, the body should be a prescriptive workflow. Tell the agent exactly what to do, in what order, with what tools.

### 4. Reference shared rule libraries

If your skill needs technical rules (Core Web Vitals thresholds, schema patterns, etc.), check `skills/shared-references/` first. If a relevant library exists, reference it instead of duplicating rules in your skill.

If the rules are unique to your skill, put them in your local `references/` folder.

### 5. Reference tool cheatsheets

If your skill uses an external tool (Ahrefs, GSC, Screaming Frog, GA4, etc.), check `skills/shared-references/tool-references/` for a cheatsheet. Reference it instead of teaching tool syntax inline.

If your skill uses a tool that doesn't have a cheatsheet yet, write one and submit it alongside your skill.

### 6. Update the README

Add your skill to the Skills Index in `README.md`.

### 7. Update VERSIONS.md

Add a line under the next version (e.g., "Unreleased") describing your skill.

### 8. Run validation

```bash
./validate-skills.sh
```

This catches missing frontmatter, broken reference paths, and other common issues.

### 9. Open a pull request

Push your branch and open a PR. Use the PR template to describe what your skill does, what triggered the need for it, and any tools or references it relies on.

## Writing Style

These rules apply to all `SKILL.md` files and reference docs:

- **Be prescriptive.** Skills tell the agent what to do, not why.
- **No em dashes.** Use colons, periods, parentheses, or commas instead.
- **No filler.** Skip phrases like "in today's landscape," "leveraging cutting-edge approaches," "comprehensive suite of."
- **Be specific.** Reference tools by name, list exact thresholds, name MCP method names where applicable.
- **Use active voice.** "Audit the page for X" beats "the page should be audited for X."
- **Keep paragraphs short.** One to four sentences. One-line paragraphs are encouraged for emphasis.

## Quality Bar

We hold contributions to these standards:

- The skill solves a real, specific problem (not a vague "improve X")
- The description is specific enough that the agent loads the skill at the right time
- The body walks the agent through a clear, repeatable workflow
- Tools and thresholds are named, not gestured at
- At least one worked example is included, either inline or in `examples/`

## Improving an Existing Skill

Small improvements (clarification, new examples, bug fixes) can go straight to a PR. Larger changes (reworking the workflow, splitting a skill into multiple skills, changing the description significantly) should start with an issue so we can discuss before you do the work.

## Adding a Shared Reference

Shared references live in `skills/shared-references/`. Add a new one when:

- The rules cover one logical topic (Core Web Vitals, redirect patterns, schema validation, etc.)
- Multiple skills will use the same rules
- The rules are factual and prescriptive, not interpretive

If only one skill uses the rules, put them in that skill's local `references/` folder instead.

## Reporting Bugs

Use the bug issue template. Include:

- Which skill is affected
- What you expected the agent to do
- What it actually did
- The agent you were using (Claude Code, Cursor, Codex, etc.)
- The prompt or context that triggered the issue

## Code of Conduct

Be respectful, be specific, be helpful. We want this repo to be a place practitioners come back to, not a battleground.

## Questions

Open an issue with the `question` label, or reach out to [Generix Marketing](https://www.generixmarketing.com/) directly.
