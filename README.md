# agent-skills

A curated collection of skills, prompts, and tooling for AI agents, with a focus on SEO, AEO, and modern marketing workflows.

Maintained by [Generix Marketing](https://www.generixmarketing.com/).

## What Are Agent Skills?

Skills are reusable instructions that teach an AI agent (like Claude) how to do a specific job well. Think of a skill as a recipe: you give the agent a folder with a `SKILL.md` file, supporting references, and optional scripts, and the agent loads it on demand when the task matches.

A skill might teach an agent how to:

- Run a technical SEO audit using Screaming Frog and Google Search Console
- Audit a page for AI citation-friendliness (extractability, structure, factual specificity)
- Generate schema markup for a service page
- Identify keyword gaps against competitor sites
- Build a Reddit presence strategy for an AEO-driven industry

The format is portable. Skills here work in Claude Code, the Claude Agent SDK, Cowork mode, and any agent that follows the [Agent Skills spec](https://agentskills.io).

## Repo Structure

```
agent-skills/
├── README.md
├── CLAUDE.md
├── AGENTS.md
├── CONTRIBUTING.md
├── VERSIONS.md
├── LICENSE
└── skills/
    ├── _foundation/         # Read by every other skill first
    │   └── client-context/
    ├── seo/                 # Traditional SEO skills
    ├── aeo/                 # AI citation and answer-engine optimization
    ├── content/             # Content strategy, schema, site architecture
    ├── analytics/           # Measurement and reporting
    └── shared-references/   # Rule libraries and tool cheatsheets
```

Each skill lives in its own folder with a `SKILL.md` at the root. Supporting files (references, scripts, examples) sit alongside it.

## Skills Index

Skills land here as they're published. The full planned list spans ~25 skills across the categories above.

| Category | Skills | Status |
|---|---|---|
| Foundation | client-context | Coming soon |
| SEO | 8 skills (foundations, on-page, technical, keyword research, competitor analysis, off-page link building, content audit, local) | Coming soon |
| AEO | 9 skills (content optimization, citation tracking, entity presence, etc.) | Coming soon |
| Content | 5 skills (strategy, programmatic SEO, schema, etc.) | Coming soon |
| Analytics | 2 skills (marketing analytics, SEO reporting) | Coming soon |

## How to Use a Skill

1. Clone the repo or copy the skill folder you want.
2. Drop the folder into your agent's skills directory:
   - **Claude Code:** `~/.claude/skills/`
   - **Claude Agent SDK:** wherever your project loads skills from
   - **Cowork mode:** install via plugin or place in your skills directory
   - **Cursor, Windsurf, Codex:** see `AGENTS.md` for cross-agent install paths
3. The agent loads the skill automatically when the task matches its description.

For a walkthrough of how skills work, read Anthropic's [Claude Skills documentation](https://docs.claude.com).

## Contributing

Contributions are welcome. If you've built a skill that solves a real problem (especially in SEO, AEO, content marketing, or analytics workflows), open a pull request.

Read `CONTRIBUTING.md` for the required folder structure, how to write a `SKILL.md` description that triggers reliably, and the quality bar we hold contributions to.

Quick version: every skill needs a clear name, a specific description (so the agent knows when to load it), and at least one worked example.

## License

[MIT](LICENSE). Use, fork, remix, ship. Attribution appreciated but not required.

## About Generix Marketing

[Generix Marketing](https://www.generixmarketing.com/) is an SEO and AEO agency that helps brands earn search visibility through technical fixes, content strategy, and answer-engine optimization. We publish skills, tools, and guides we use in our own client work.

If a skill in this repo saved you time, we'd love to hear about it.
