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
| Foundation | [client-context](skills/_foundation/client-context/) | Shipped |
| SEO | 8 skills (foundations, on-page, technical, keyword research, competitor analysis, off-page link building, content audit, local) | Coming soon |
| AEO | 9 skills (content optimization, citation tracking, entity presence, etc.) | Coming soon |
| Content | 5 skills (strategy, programmatic SEO, schema, etc.) | Coming soon |
| Analytics | 2 skills (marketing analytics, SEO reporting) | Coming soon |

## Quick Start

Here is how to go from "I just found this repo" to "the agent is doing real work for me" in under five minutes.

### 1. Pick your agent

These skills work in any agent that follows the [Agent Skills spec](https://agentskills.io). The setup path varies slightly:

- **Claude Code (terminal):** install from [claude.ai/code](https://claude.ai/code), then place skills in `~/.claude/skills/`
- **Cowork mode (Claude desktop app):** install Claude Desktop, then drop skills in your configured skills directory
- **Cursor:** place skills in `.cursor/skills/` inside your project
- **Windsurf:** place skills in `.windsurf/skills/` inside your project
- **OpenAI Codex:** place skills in `.agents/skills/` inside your project

### 2. Install a skill

The fastest path is to clone the repo and copy the skill folder you want:

```bash
git clone https://github.com/Generix-Marketing/agent-skills.git
cp -r agent-skills/skills/_foundation/client-context ~/.claude/skills/
```

If you only want one skill, use [degit](https://github.com/Rich-Harris/degit) to pull it without cloning the whole repo:

```bash
npx degit Generix-Marketing/agent-skills/skills/_foundation/client-context ~/.claude/skills/client-context
```

### 3. Start with the foundation skill

Always install `_foundation/client-context` first. Other skills read from the `client-context.md` file it creates, so they need it in place to work properly.

### 4. Run your first prompt

Open your agent in a working directory for your client (a folder you will come back to). Try a prompt that matches a skill description:

```
Let's set up client context for Cardinal Ridge Roofing, https://www.example.com/
```

The agent detects that `client-context` matches your prompt, loads the skill, walks you through the intake questions, and writes `client-context.md` to your working directory. From then on, every other skill you install reads from that file as the starting point.

### 5. Add more skills as you need them

You do not need to install every skill at once. Add them as your work calls for them: a technical audit skill when you need to crawl a site, a keyword research skill when you are planning content, an AEO skill when you are auditing for AI citations. Each one loads automatically when your prompt matches its description.

For a deeper walkthrough of how skills work, read Anthropic's [Claude Skills documentation](https://docs.claude.com). To write your own skill, jump to `CONTRIBUTING.md`.

## Contributing

Contributions are welcome. If you've built a skill that solves a real problem (especially in SEO, AEO, content marketing, or analytics workflows), open a pull request.

Read `CONTRIBUTING.md` for the required folder structure, how to write a `SKILL.md` description that triggers reliably, and the quality bar we hold contributions to.

Quick version: every skill needs a clear name, a specific description (so the agent knows when to load it), and at least one worked example.

## License

[MIT](LICENSE). Use, fork, remix, ship. Attribution appreciated but not required.

## About Generix Marketing

[Generix Marketing](https://www.generixmarketing.com/) is an SEO and AEO agency that helps brands earn search visibility through technical fixes, content strategy, and answer-engine optimization. We publish skills, tools, and guides we use in our own client work.

If a skill in this repo saved you time, we'd love to hear about it.
