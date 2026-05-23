# Versions

Changelog for agent-skills. Follows [semantic versioning](https://semver.org/) loosely: major versions for breaking changes (skill renames, removed skills), minor for new skills, patch for fixes and clarifications.

## Unreleased

Next: foundational SEO skills (seo-foundations, on-page audit, technical audit).

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
