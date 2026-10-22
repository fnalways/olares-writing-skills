---
name: olares-writing-skills
description: |
  Writing and customer-support skills for Olares contributors. Use when the user wants to create or edit documentation, use case tutorials, troubleshooting guides, UX copy, or evidence-backed customer-service replies for Olares. Triggers on phrases like "write documentation", "create a use case", "turn porting notes into a tutorial", "translate docs", "review UI strings", "write troubleshooting guide", "review this ticket reply", "Olares support", "Olares docs", and "docs.olares.com". Includes skills for: olares-docs-writer, use-case-writer, olares-ux-writing, olares-i18n-audit, and olares-customer-service.
metadata:
  version: 0.4.0
---

# Olares Writing Skills

Collection of writing skills for Olares documentation and UI copy.

## Included Skills

- **olares-docs-writer**: Write Olares manuals, developer docs, and troubleshooting in VitePress format. Route app use cases to use-case-writer. Bilingual EN/ZH.
- **use-case-writer**: Create task-oriented bilingual use case tutorials from drafts, porting notes, test records, or PRs for docs.olares.com, with English-first review and complete Chinese delivery after finalization.
- **olares-ux-writing**: Review and write bilingual UI copy (labels, errors, dialogs, onboarding) following Olares-specific style and terminology.
- **olares-i18n-audit**: Check i18n consistency across Olares documentation.
- **olares-customer-service**: Research, triage, draft, and review Olares customer-support replies using current official evidence and risk-aware escalation.

## Usage

Ask your agent to help with Olares writing tasks:
- "Write a use case tutorial for installing Ollama on Olares"
- "Translate this Chinese draft into an Olares use case"
- "Turn these app-porting notes and test results into an Olares use case"
- "Review these UI strings against Olares UX writing guidelines"
- "Write a troubleshooting guide for VPN connection issues"
- "Check this doc for i18n consistency"
- "Research this Olares ticket and draft a safe customer reply"

## File Structure

```
skills/
├── olares-docs-writer/   # Main documentation skill
├── use-case-writer/      # Bilingual use case transformation
├── olares-ux-writing/    # UI copy review
├── olares-i18n-audit/    # i18n audit
└── olares-customer-service/ # Support reply research and review
```

For detailed skill documentation, see individual skill directories under `skills/`.
