# AGENTS.md

Guidelines for AI agents working in this repository.

## Repository Overview

This repository contains **Agent Skills** for Olares contributors, following the [Agent Skills specification](https://agentskills.io/specification.md). Skills install to `.agents/skills/` (cross-agent standard) or `.claude/skills/` (Claude Code). This repo also serves as a Claude Code plugin marketplace via `.claude-plugin/marketplace.json`.

- **Name**: Olares Writing Skills
- **GitHub**: [fnalways/olares-writing-skills](https://github.com/fnalways/olares-writing-skills)
- **License**: MIT

## Repository Structure

```
olares-writing-skills/
├── .claude-plugin/
│   ├── plugin.json         # Claude Code plugin manifest
│   └── marketplace.json    # Claude Code marketplace manifest
├── skills/
│   ├── olares-docs-writer/
│   │   ├── SKILL.md        # Required, < 500 lines
│   │   └── references/     # Detailed templates, examples, style guides
│   ├── use-case-writer/
│   └── olares-ux-writing/
├── AGENTS.md
├── CLAUDE.md               # Mirror of AGENTS.md for Claude Code
├── CONTRIBUTING.md
├── LICENSE
├── README.md
├── VERSIONS.md
└── validate-skills.sh      # Spec compliance check
```

## Build / Lint / Test Commands

Skills are content-only (no build step). Validate before committing:

```bash
./validate-skills.sh
```

This checks:
- YAML frontmatter is present and valid
- `name` field matches the directory name exactly
- `name` is 1-64 chars, lowercase alphanumeric + hyphens
- `description` is 1-1024 chars and includes trigger phrases
- `version` (if present) sits under `metadata:`, not at the top level
- SKILL.md is < 500 lines (longer content goes into `references/`)

## Agent Skills Specification

Skills follow the [Agent Skills spec](https://agentskills.io/specification.md). Required frontmatter:

```yaml
---
name: skill-name                    # Must match directory name
description: |
  When the user wants to ... use this skill ...
  Triggers on phrases like ...
metadata:
  version: 0.1.0                    # Semver
---
```

## Adding a New Skill

1. Create `skills/<name>/SKILL.md` with valid frontmatter.
2. Write the SKILL.md body (under 500 lines). Long templates and examples go in `skills/<name>/references/`.
3. Add the skill path to `.claude-plugin/marketplace.json` under `plugins[0].skills`.
4. Run `./validate-skills.sh` and fix any errors.
5. Update VERSIONS.md.
6. Bump `metadata.version` in the new SKILL.md and `version` in `plugin.json` / `marketplace.json` as appropriate.

## Editing an Existing Skill

1. Edit `skills/<name>/SKILL.md` or files under `skills/<name>/references/`.
2. Bump `metadata.version` in the SKILL.md frontmatter (semver: minor for additions, patch for fixes).
3. Append an entry to VERSIONS.md.
4. Run `./validate-skills.sh`.
5. Bump `version` in `plugin.json` and `marketplace.json` only if the user-visible plugin surface changes (skill added, removed, or major behavior change).

## Style Conventions

- Trigger phrases in `description` should cover both formal (("when the user wants to...")) and casual ("the user just says X") forms.
- When a skill references files in its own `references/` directory, use relative paths from the skill root: `references/document-types/use-case.md`.
- Every skill should mention its scope boundaries ("For X, see Y") to reduce false triggering.
