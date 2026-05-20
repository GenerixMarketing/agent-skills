# agent-skills

A curated collection of skills, prompts, and tooling for AI agents, with a focus on SEO, AEO, and modern marketing workflows.

Maintained by [Generix Marketing](https://generixmarketing.com).

## What Are Agent Skills?

Skills are reusable instructions that teach an AI agent (like Claude) how to do a specific job well. Think of a skill as a recipe: you give the agent a folder with a `SKILL.md` file, supporting references, and optional scripts, and the agent loads it on demand when the task matches.

A skill might teach an agent how to:

- Run a technical SEO audit using Screaming Frog and Google Search Console
- Write blog content in a specific brand voice
- Generate schema markup for a service page
- Pull a keyword opportunity report from Ahrefs or SEMRush
- Format a site breakdown deliverable for a client

The format is portable. Most skills here work in Claude Code, the Claude Agent SDK, and Cowork mode without modification.

## Repo Structure

```
agent-skills/
├── README.md
├── LICENSE
├── CONTRIBUTING.md
└── skills/
    ├── seo-audit/
    │   ├── SKILL.md
    │   └── references/
    ├── keyword-research/
    │   └── SKILL.md
    └── ...
```

Each skill lives in its own folder under `/skills/` with a `SKILL.md` at the root. Supporting files (reference docs, scripts, examples) sit alongside it.

## Skills Index

| Skill | What It Does | Best For |
|---|---|---|
| _Coming soon_ | _First skills land here as they're published_ | _TBD_ |

## How to Use a Skill

1. Clone the repo or copy the skill folder you want.
2. Drop the folder into your agent's skills directory:
   - **Claude Code:** `~/.claude/skills/`
   - **Claude Agent SDK:** wherever your project loads skills from
   - **Cowork mode:** install via plugin or place in your skills directory
3. The agent will load the skill automatically when the task matches its description.

For a walkthrough of how skills work, read Anthropic's [Claude Skills documentation](https://docs.claude.com).

## Contributing

Contributions are welcome. If you've built a skill that solves a real problem (especially in SEO, AEO, content marketing, or analytics workflows), open a pull request.

Before submitting, read `CONTRIBUTING.md` for:

- The required folder structure for a new skill
- How to write a `SKILL.md` description that triggers reliably
- Quality bar for examples, references, and scripts
- Style guidelines for the README in your skill folder

Quick version: every skill needs a clear name, a specific description (so the agent knows when to load it), and at least one worked example.

## License

[MIT](LICENSE). Use, fork, remix, ship. Attribution appreciated but not required.

## About Generix Marketing

[Generix Marketing](https://generixmarketing.com) is an SEO and AEO agency that helps brands earn search visibility through technical fixes, content strategy, and answer-engine optimization. We publish skills, tools, and guides we use in our own client work.

If a skill in this repo saved you time, we'd love to hear about it.
