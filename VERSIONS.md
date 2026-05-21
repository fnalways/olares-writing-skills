# Versions

Plugin-level changelog. Per-skill changes show up in the SKILL.md `metadata.version` field.

## v0.2.0 — 2026-05-21

- `use-case-writer` v0.2.0:
  - Remove the optional `authors` frontmatter field. New use cases no longer include `authors`.
  - Add a top-level **Deliverables** section listing all four required outputs (English md, Chinese `@include` stub, EN sidebar entry, ZH sidebar entry) so the multi-file nature of a use case is visible up front.
  - Rename Process step 6 to **Create remaining deliverables (REQUIRED, not optional)** and reorder it so the Chinese stub is created first, ahead of the sidebar updates.
  - Add Process step 7, a four-item verification checklist the agent must confirm before reporting completion.
  - Update the skill `description` to state that each use case is a multi-file deliverable.

## v0.1.0 — 2026-05-06

Initial release. Three skills:

- `olares-docs-writer` v0.1.0: Olares documentation writer (use cases, manuals, developer docs, troubleshooting). Bilingual EN/ZH.
- `use-case-writer` v0.1.0: Chinese-to-English Olares use case tutorial transformer.
- `olares-ux-writing` v0.1.0: Bilingual UX copy reviewer for Olares products.
