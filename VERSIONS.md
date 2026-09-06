# Versions

Plugin-level changelog. Per-skill changes show up in the SKILL.md `metadata.version` field.

## v0.4.0 — 2026-09-06

- Add `olares-customer-service` v0.1.0:
  - Research current official Olares documentation, Known Issues, Release Notes, and traceable engineering confirmation before making technical claims.
  - Draft and review customer replies with explicit verification, failure branches, source attribution, and content-gap reporting.
  - Apply risk-aware escalation for data loss, reinstall, firmware/BIOS, hardware, security, privacy, account recovery, licensing, refund, and warranty cases.
  - Treat historical ticket replies as directional evidence rather than a trusted answer corpus.
- Update the root `olares-writing-skills` skill to v0.2.0 and expose the new skill through the plugin marketplace.

## v0.3.0 — 2026-07-16

- `olares-docs-writer` v0.2.0:
  - Add an **SEO metadata guidelines** section: the `<title>` tag vs H1 (only override an over-long H1, otherwise default to the H1), meta description (required, unique, under 160 characters), keywords via the `head` block, `noindex` vs `search: false`, the redirect workflow for renaming/retiring pages, and the Cloudflare email-obfuscation note.
  - Update Best Practices to require a unique description and to only override a long H1 with a frontmatter `title`.
  - Expand the frontmatter example and notes in `references/markdown-conventions.md` to match.
- `olares-ux-writing` v0.1.5:
  - Add the convention for spacing around embedded Latin text (brand names, product terms) inside CJK copy: zh-CN keeps a half-width space, ja-JP does not, and it must not be carried over between the two languages.

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
