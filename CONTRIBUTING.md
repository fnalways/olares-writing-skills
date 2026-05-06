# Contributing

Thanks for considering a contribution. This repo follows the [Agent Skills spec](https://agentskills.io/specification.md), so the rules below align with the broader ecosystem.

## Adding a New Skill

1. Create a new directory under `skills/<skill-name>/`. The name must:
   - Be 1-64 characters
   - Use only lowercase letters, digits, and hyphens
   - Match the directory name exactly

2. Add `skills/<skill-name>/SKILL.md`:

   ```markdown
   ---
   name: skill-name
   description: |
     When the user wants to [primary task], use this skill ...
     Triggers on phrases like "[example]", "[another example]" ...
     For [related task], see `[other-skill]`.
   metadata:
     version: 0.1.0
   ---

   # Skill body (< 500 lines total)
   ```

3. Place long templates, examples, and reference material under `skills/<skill-name>/references/`. The SKILL.md should link to those files using relative paths.

4. Add the new skill path to `.claude-plugin/marketplace.json`:

   ```json
   "skills": [
     "./skills/skill-name"
   ]
   ```

5. Run validation:

   ```bash
   ./validate-skills.sh
   ```

   Fix any errors before committing. Warnings (e.g., missing trigger phrases) are also worth addressing.

6. Bump versions if needed (see below) and add a line to VERSIONS.md.

## Editing an Existing Skill

1. Make your changes to `SKILL.md` or files under `references/`.
2. Bump `metadata.version` in the SKILL.md frontmatter using [semver](https://semver.org/):
   - **Patch** (`0.1.0 → 0.1.1`): typo fixes, minor wording, internal cleanup
   - **Minor** (`0.1.0 → 0.2.0`): new doc type, new template, new trigger
   - **Major** (`0.1.0 → 1.0.0`): breaking change in skill behavior or output format
3. Append an entry to VERSIONS.md.
4. Run `./validate-skills.sh`.
5. If the change adds or removes a skill, or changes plugin-level behavior, also bump `version` in `.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json`.

## Local Development

The cleanest setup is to symlink your live skills directory to this repo so edits are picked up immediately by your agent:

```bash
# One-time setup
ln -s ~/olares-writing-skills/skills/olares-docs-writer ~/.claude/skills/olares-docs-writer
ln -s ~/olares-writing-skills/skills/use-case-writer ~/.claude/skills/use-case-writer
ln -s ~/olares-writing-skills/skills/olares-ux-writing ~/.claude/skills/olares-ux-writing
```

After that, edit a SKILL.md in this repo, then trigger the skill in any project to test.

## Pre-commit Validation (Optional)

Wire `validate-skills.sh` into a git hook so violations block commits:

```bash
echo '#!/bin/bash
./validate-skills.sh' > .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

## Pull Requests

- Keep each PR focused on a single skill change when possible
- Include "before/after" examples in the PR description for behavioral changes
- Link any related Olares docs or design references

## License

By contributing, you agree your contributions are licensed under MIT.
