---
name: olares-writing-skills
description: |
  Writing and customer-support skills for Olares contributors. Use when the user wants to create or edit documentation, use case tutorials, troubleshooting guides, UX copy, or evidence-backed customer-service replies for Olares. Triggers on phrases like "write documentation", "create a use case", "translate docs", "review UI strings", "write troubleshooting guide", "review this ticket reply", "Olares support", "Olares docs", and "docs.olares.com". Includes skills for: olares-docs-writer, use-case-writer, olares-ux-writing, olares-i18n-audit, and olares-customer-service.
metadata:
  version: 0.2.0
---

# Olares Writing Skills

Collection of writing skills for Olares documentation and UI copy.

## Included Skills

- **olares-docs-writer**: Write Olares documentation in VitePress format (use cases, manuals, developer docs, troubleshooting). Bilingual EN/ZH.
- **use-case-writer**: Transform Chinese drafts into polished English use case tutorials for docs.olares.com.
- **olares-ux-writing**: Review and write bilingual UI copy (labels, errors, dialogs, onboarding) following Olares-specific style and terminology.
- **olares-i18n-audit**: Check i18n consistency across Olares documentation.
- **olares-customer-service**: Research, triage, draft, and review Olares customer-support replies using current official evidence and risk-aware escalation.

## Usage

Ask your agent to help with Olares writing tasks:
- "Write a use case tutorial for installing Ollama on Olares"
- "Translate this Chinese draft into an Olares use case"
- "Review these UI strings against Olares UX writing guidelines"
- "Write a troubleshooting guide for VPN connection issues"
- "Check this doc for i18n consistency"
- "Research this Olares ticket and draft a safe customer reply"

## File Structure

```
skills/
├── olares-docs-writer/   # Main documentation skill
├── use-case-writer/      # Chinese to English translation
├── olares-ux-writing/    # UI copy review
├── olares-i18n-audit/    # i18n audit
└── olares-customer-service/ # Support reply research and review
```

For detailed skill documentation, see individual skill directories under `skills/`.
