# Olares Writing Skills

Writing and customer-support skills for [Olares](https://olares.com) contributors. Drop these into your AI coding agent so it can help draft Olares documentation, use case tutorials, UX copy, and evidence-backed customer replies in the established Olares style.

Built for Claude Code, OpenAI Codex, Cursor, Windsurf, and any agent that supports the [Agent Skills spec](https://agentskills.io).

## What's Inside

| Skill | What it does |
| --- | --- |
| `olares-docs-writer` | Write Olares documentation in VitePress format (use cases, manuals, developer docs, troubleshooting). Bilingual EN/ZH. |
| `use-case-writer` | Transform Chinese drafts into polished English use case tutorials for `docs.olares.com`. |
| `olares-ux-writing` | Review and write bilingual UI copy (labels, errors, dialogs, onboarding) following Olares-specific style and terminology. |
| `olares-customer-service` | Research, triage, draft, and review Olares support replies using current official evidence and risk-aware escalation rules. |

## Installation

### Option 1: `npx skills` (Recommended)

Use the [`vercel-labs/skills`](https://github.com/vercel-labs/skills) CLI:

```bash
# Install all writing skills
npx skills add fnalways/olares-writing-skills

# Install a specific skill
npx skills add fnalways/olares-writing-skills --skill olares-docs-writer

# List available skills
npx skills add fnalways/olares-writing-skills --list
```

This installs to `.agents/skills/` and symlinks into `.claude/skills/` for Claude Code compatibility.

### Option 2: Claude Code Plugin

```
/plugin marketplace add fnalways/olares-writing-skills
/plugin install olares-writing-skills
```

### Option 3: Clone and Copy

```bash
git clone https://github.com/fnalways/olares-writing-skills ~/olares-writing-skills
cp -r ~/olares-writing-skills/skills/* ~/.claude/skills/
```

### Option 4: Git Submodule

```bash
git submodule add https://github.com/fnalways/olares-writing-skills .claude/skills/olares-writing-skills
```

### Option 5: OpenClaw

Install via OpenClaw's git-based skill installation:

```bash
openclaw skills install git:fnalways/olares-writing-skills --global
```

For specific branches or versions:

```bash
openclaw skills install git:fnalways/olares-writing-skills@branch-name --global
openclaw skills install git:fnalways/olares-writing-skills --version 1.0.0 --global
```

## Usage

Once installed, just ask your agent to help with Olares writing tasks:

- "Write a use case tutorial for installing Ollama on Olares"
- "Translate this Chinese draft into an Olares use case"
- "Review these UI strings against Olares UX writing guidelines"
- "Write a troubleshooting guide for VPN connection issues"
- "Research this Olares ticket and draft a safe customer reply"

The agent picks the right skill based on the trigger phrases in your request.

## Versioning

Each skill carries its own `metadata.version` in the SKILL.md frontmatter. The plugin overall is versioned via `.claude-plugin/plugin.json`. See [VERSIONS.md](./VERSIONS.md) for changelog.

## Contributing

PRs welcome. See [CONTRIBUTING.md](./CONTRIBUTING.md) for the workflow, validation requirements, and version-bump conventions.

## License

[MIT](./LICENSE).
