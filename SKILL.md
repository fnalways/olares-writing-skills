---
name: olares-writing-skills
description: Writing skills for Olares contributors. Use when the user wants to create or edit documentation, use case tutorials, troubleshooting guides, or UI copy for Olares. Triggers on phrases like "write documentation", "create a use case", "translate docs", "review UI strings", "write troubleshooting guide", "Olares docs", "docs.olares.com". Includes skills for: olares-docs-writer (VitePress documentation in EN/ZH), use-case-writer (Chinese to English use case tutorials), olares-ux-writing (UI labels, errors, dialogs), olares-i18n-audit (i18n consistency checks).
metadata:
  version: 0.1.0
---

# Olares Writing Skills

Collection of writing skills for Olares documentation and UI copy.

## Included Skills

- **olares-docs-writer**: Write Olares documentation in VitePress format (use cases, manuals, developer docs, troubleshooting). Bilingual EN/ZH.
- **use-case-writer**: Transform Chinese drafts into polished English use case tutorials for docs.olares.com.
- **olares-ux-writing**: Review and write bilingual UI copy (labels, errors, dialogs, onboarding) following Olares-specific style and terminology.
- **olares-i18n-audit**: Check i18n consistency across Olares documentation.

## Usage

Ask your agent to help with Olares writing tasks:
- "Write a use case tutorial for installing Ollama on Olares"
- "Translate this Chinese draft into an Olares use case"
- "Review these UI strings against Olares UX writing guidelines"
- "Write a troubleshooting guide for VPN connection issues"
- "Check this doc for i18n consistency"

## File Structure

```
skills/
├── olares-docs-writer/   # Main documentation skill
├── use-case-writer/      # Chinese to English translation
├── olares-ux-writing/    # UI copy review
└── olares-i18n-audit/    # i18n audit
```

For detailed skill documentation, see individual skill directories under `skills/`.
