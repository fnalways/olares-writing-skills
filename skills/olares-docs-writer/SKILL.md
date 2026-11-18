---
name: olares-docs-writer
description: Write Olares documentation in English and Chinese for the VitePress docs site. Use when the user wants to create or edit manuals, developer docs, troubleshooting guides, FAQ entries, or translations between English and Chinese, and when they mention `docs.olares.com`, `docs/manual/`, `docs/developer/`, or `docs/manual/help/`. Enforces the Olares style guide and VitePress conventions. For app use case tutorials from any source, including porting notes and test records, use use-case-writer instead. For UI strings and product copy, see olares-ux-writing.
metadata:
  version: 0.3.1
---

# Olares Documentation Writer

This skill helps you write documentation for Olares that matches the official style and format.

## Overview

Olares documentation uses VitePress with these key characteristics:

- **Dual language support**: English (default) and Chinese (under `/zh/`)
- **Use cases**: Practical tutorials for apps and workflows
- **Manual**: User guides and feature documentation
- **Developer docs**: Technical documentation for developers
- **Troubleshooting**: Problem-solution guides under `/docs/manual/help/`

## Document Types

### 1. Use Case Tutorial

Route all app use cases to `use-case-writer`, regardless of source language or whether the input is a draft, porting log, test result, or PR. It owns the task-oriented workflow, required Learning objectives, reusable fragments, version metadata, and bilingual delivery when in scope. Do not use the generic examples or warning rules here to override that skill's current requirements.

### 2. Manual/Guide Documentation

Feature explanations and user guides.

Choose sections that help the reader complete the task. Use a "When to use this" explanation when similar guides or starting states could cause confusion. Add concept, feature, configuration, or error guidance only when it affects the reader's choices or actions. Explain irreversible consequences next to the action.

### 3. Index Pages

The use cases index uses `<UseCaseGallery />` and reads entries from `docs/.vitepress/data/useCases.ts`. For a new app use case, follow `use-case-writer` to update the gallery data and the sidebar entries for the languages in scope. Do not add a hard-coded `FilterableList` to the use cases index.

### 4. Developer Documentation

Technical documentation for developers, including architecture, API references, and development guides.

**Sub-types:**

- **A. Architecture/Concept Documentation**: Explains system design, components, and how things work. Uses diagrams and technical terminology. Target audience: system administrators, developers.
- **B. API/Configuration Reference**: Detailed field descriptions, options, and valid values. Uses tables for structured data. Code examples in multiple formats.
- **C. Development Tutorials**: Step-by-step guides for building apps or features. Hands-on approach with working examples.

For developer-doc-specific markdown patterns (line-highlighted YAML, field reference tables, architecture diagrams, cross-references), see `references/developer-conventions.md`. For full samples, see `references/examples/developer-architecture.md` and `references/examples/developer-api.md`.

### 5. Troubleshooting Documentation

Problem-solution guides for diagnosing and resolving issues. Use a problem-focused title, then `## Condition`, `## Cause`, `## Solution`, optional `## Prevention`. Use the `ts-` filename prefix and place files under `/docs/manual/help/` (English) and `/docs/zh/manual/help/` (Chinese).

For the full template, section guidelines, complex diagnostic step structure, and platform-specific patterns (macOS / Windows), see `references/document-types/troubleshooting.md`.

## H1 title guidelines

Each page's H1 (`#`) is used as the page title in search results, so it must be unique across the site. Duplicate H1 titles (e.g., several pages all titled "Common issues" or "Known issues") hurt SEO and confuse readers.

- **Make every H1 unique and specific.** Add the app name, product area, or scenario that scopes the page. Prefer "Open WebUI common issues" over "Common issues", "Olares One known issues" over "Known issues".
- **Check for duplicates before finalizing** a new or renamed page. List existing duplicate H1s with:
  ```bash
  find docs -type f -name '*.md' -not -path '*/node_modules/*' | xargs grep -h '^# ' | sort | uniq -d
  ```
- **English/Chinese pairs are expected.** When the Chinese page reuses the English content via `@include`, or is a direct translation, the same H1 in `docs/` and `docs/zh/` is fine. Only same-language collisions need fixing.
- **CLI command reference pages** named after the command itself (e.g., `` `install` ``, `` `backup` ``) are an accepted exception, since the command name is the H1.
- When you rename an H1, the change is local to that line. Cross-references in other docs use file paths and link text, so they are not affected. Do not edit link text to match unless the link text is now misleading.

## SEO metadata guidelines

Every page ships three search-facing fields: the `<title>` tag, the meta `description`, and optional `keywords`. Set them deliberately for every new or edited page, in **both** languages.

### The `<title>` tag and over-long H1s

VitePress builds the `<title>` tag from the frontmatter `title` if present, otherwise from the first H1.

- **Default to the H1.** When the H1 already works as the title, do **not** add a `title` field — VitePress uses the H1 automatically. Don't add a redundant `title` that just repeats the H1.
- **Only override an over-long H1.** If the H1 has to stay long or descriptive for on-page clarity, add a shorter `title` in frontmatter (aim for ~60 chars) to override **only** the `<title>` tag — the visible H1 is unchanged:
  ```yaml
  ---
  title: Manage accelerator resources        # only because the H1 below is long
  description: ...
  ---
  # Manage GPU, integrated accelerators, and CPU fallback on Olares
  ```
- Keep titles **unique** within a language (see H1 title guidelines). Two pages with the same `<title>` compete against each other in search.

### Meta description

- **Required and unique** on every page. Duplicate descriptions hurt SEO the same way duplicate titles do.
- Length: **keep under 160 characters** (both languages). Front-load the key info — the tail gets truncated in results.
- Write a real sentence that summarizes the page and earns the click. Don't keyword-stuff.
- This is the right home for positioning/brand terms that don't belong in the H1 (e.g., "self-hosted", "Google Photos alternative").
- YAML quoting: only quote the value when it contains a YAML-special sequence — a colon-followed-by-space, or a leading `>`, `|`, `#`, `&`, `*`, `[`, `{`, `"`, `'`. Plain prose needs no quotes.

### Keywords

Optional, via a `head` block. Use a short, comma-separated set, and put competitor/alternative and long-tail terms here instead of forcing them into the H1:
```yaml
head:
  - - meta
    - name: keywords
      content: Olares, self-hosted photos, Immich, Google Photos alternative
```

### Content length: quality over arbitrary thresholds

Do not pad text, add filler sections, or inflate descriptions just because an SEO plugin flags a page as "too short." Documentation length should be determined by the topic's actual complexity and what the user needs to succeed.

- A simple one-step guide should stay short.
- A complex multi-app workflow deserves the space it needs.
- If a plugin reports thin content, first check whether steps are missing or unclear — not whether the word count is high enough.

### Keep H1s natural — push positioning terms to metadata

Do **not** stuff "Olares" or "X alternative" into the H1 just for keywords. Write the H1 for the reader and move those terms to `description`/`keywords`:
- ❌ `# Self-host your photos with Immich (Google Photos alternative)`
- ✅ `# Manage photos with Immich` — with "self-hosted" / "Google Photos alternative" carried in `description` and `keywords`.

### `noindex` vs. `search: false`

- `search: false` only removes a page from the **on-site** search box. It does **not** stop Google/Bing from indexing it.
- To keep a page out of search engines, add `noindex: true` (emits `<meta name="robots" content="noindex, nofollow">`).
- Apply `noindex: true` to: `@include`-only fragment pages, outdated/superseded pages kept only for reference, and low-value pages not linked from any sidebar nav. `noindex` is reversible — remove it later to let the page be indexed again.
- Keep EN and ZH in sync: if you `noindex` a page, do the same for its counterpart.

### Renaming or retiring a page (redirects)

`docs/.vitepress/theme/redirects.ts` is the single source of truth for redirects.
- **Renaming a slug** (for a clearer or brand URL): add a permanent 301 from the old path to the new one (EN **and** ZH), update every internal link and the sidebar nav configs, then regenerate the edge config:
  ```bash
  SYNC_NGINX_REDIRECTS=1 node docs/.vitepress/scripts/sync-redirects.mjs
  ```
- **Retiring a page**: add a 301 to its closest live replacement, **delete the source `.md`** (don't leave a page that both builds and 301s), and remove or repoint any inbound links and nav entries. Pick a real, indexable redirect target — not a page that is itself `noindex` or an `@include` fragment.
- Redirect *source* paths are auto-excluded from `sitemap.xml`, so a renamed/retired URL won't show up as a redirecting sitemap entry.

### Example emails are rewritten by Cloudflare

Example addresses like `alice@olares.com` in a page are rewritten by Cloudflare Email Address Obfuscation into `/cdn-cgi/l/email-protection` links, which crawlers report as "broken." This is fixed at the Cloudflare layer (disable Email Obfuscation for `/docs/*`), not in the markdown — so realistic example IDs are fine. Just don't publish a real, monitored inbox as plain text unless that's intended.

## Writing Style

### English Style

- **Tone**: Professional but natural and conversational. Write like you're explaining to a colleague, not writing a formal report.
- **Voice**: Active voice, second person ("you")
- **Sentence structure**: Clear, concise, and direct. Get to the point quickly.
- **Headings**: Use gerunds ("Installing", "Configuring") or noun phrases
- **Steps**: Start with action verbs ("Click", "Enter", "Select")

#### Writing for Readability

**Use simple, everyday words:**
- "computer" not "client device"
- "use" not "utilize"
- "start" not "initiate"
- "end" not "terminate"
- "check" not "verify" (unless verification is the specific action)

**Be direct and action-oriented:**
- ❌ "You will need to slightly modify the URL you copied earlier"
- ✅ "Modify the URL slightly"

**Avoid filler phrases:**
- ❌ "In order to" → ✅ "To"
- ❌ "It is important to note that" → Remove entirely or just state the fact
- ❌ "As mentioned previously" → Just restate briefly or use a link
- ❌ "Please be advised that" → Just say it

**Write naturally:**
- ❌ "Based on whether your computer and Olares device are on the same network, the connection process is different"
- ✅ "The connection steps depend on whether your computer and Olares device are on the same network"

**Avoid awkward dashes as separators in sentences:**
- ❌ "This is expected—the next section will guide you through installing them"
- ✅ "This is expected. The next section will guide you through installing them."

**Focus on the user's goal, not the mechanism:**
- ❌ "This guide will show you how to connect a locally hosted ComfyUI instance on Olares to Krita running on a separate computer"
- ✅ "This guide shows you how to generate AI artwork directly within Krita using ComfyUI running on Olares"

### Chinese Style

- **Tone**: Professional but slightly more casual
- **Voice**: Direct, sometimes omitting subject
- **Sentence structure**: Shorter sentences than English
- **Headings**: Concise, often shorter than English equivalent
- **Steps**: Direct instructions ("点击", "输入", "选择")

#### Write Chinese that sounds natural

Chinese docs must read like they were written in Chinese, not translated from English. The English and Chinese versions are parallel deliverables: write each one in its own language and rhythm.

- **Do not write English first and then translate sentence by sentence.** If the source is English, re-express the meaning in natural Chinese. If the source is Chinese, re-express it in natural English.
- **Read every Chinese sentence aloud.** If it feels awkward or textbook-like, rewrite it the way you would explain it to a colleague.
- **Lead with verbs, not noun phrases.** Descriptions of skills, features, or steps should start with what the user can do.
- **Remove bureaucratic, manual-style, or machine-translated filler.** Avoid vague words such as "进行", "相关", "对应", "相应", "比较", and empty phrases such as "...即可", "...的做法" unless they genuinely help clarity.
- **Explain technical terms the first time they appear.** Use backticks for the term and plain Chinese for the meaning, e.g. "选择范围：`global`（全局）或 `project`（项目级）".

## Error-Prevention Design

Help readers avoid consequential mistakes without filling the page with defensive statements. Give each constraint or consequence once, where it affects a decision.

### 1. State gating at entry

Before steps begin, state a required starting state when it could be missed:

- Use a `:::warning` at the top only when starting in the wrong state could cause serious loss or make the procedure impossible. For ordinary prerequisites, use a short sentence or list.
- If two states require completely different flows, create two documents and let users choose at the index level. Do not mix incompatible paths in one tutorial.
- Never bury a hard constraint in a Prerequisites bullet list alone.

### 2. Prevent mistakes before they happen

Within steps, prevent likely mistakes supported by the task evidence:

- Use a brief instruction or note beside the action. Use a warning only when the consequence warrants one.
- State what not to do only when it prevents a concrete mistake. Do not restate validation already performed clearly by the UI.
- Add a check after an action only when its result determines whether the reader should continue, wait, or recover.

### 3. Guard irreversible actions

For an instructed action that permanently deletes data, binds an account, or cannot be undone, give the reader:

- A `:::warning` callout before the step.
- A clear description of the consequence.
- A link to the escape route (for example, how to back up or how to factory reset).

For routine reminders, such as a page refresh clearing an unsaved conversation, use concise prose before the relevant action instead of a warning callout.

### 4. Use the correct admonition type

Choose the admonition type based on the consequence of ignoring it:

- `:::warning` — Hard constraints and irreversible actions with serious consequences. Place it at the decision point and do not repeat the same warning without a new decision.
- `:::info` — Background context, optional paths, or supplementary details that don't block the main flow.
- `:::tip` — Efficiency improvements, shortcuts, or best practices.

Never place a hard constraint in an `:::info` box.

### 5. Review checklist

Before submitting a document, ask these questions:

1. What state is the user most likely in when they open this page? Did I help them confirm this is the right guide?
2. If a user skips Prerequisites and jumps to Step 1, will they fail? If yes, put the necessary condition beside the action or add a state gate when the consequence is serious.
3. Which mistake is likely and consequential? Is the guidance beside that action and proportional to the consequence?
4. Are there any irreversible actions? Did I warn the user before they reach that step?
5. After critical steps, did I tell the user how to verify they are on track?

## Markdown Conventions

For VitePress markdown syntax (frontmatter, headings, admonitions, images, icons, code blocks, lists, tables, links), see `references/markdown-conventions.md`.

Three Olares-specific rules to keep in mind:

- **Bullet labels with bold**: Use bold only when a label acts as a category header (`- **Hardware**: ...`). Do NOT bold for emphasis in body text or in admonition labels (`**Verify changes:**` inside a warning).
- **Frontmatter required fields**: Every page needs `description`. Most pages also need `outline: [2, 3]`.
- **Admonition types**: Choose based on consequence, not emphasis. `:::warning` for hard constraints and irreversible actions. `:::info` for supplementary context. `:::tip` for efficiency improvements. Never bury a hard constraint in `:::info`.

For a general link to an upstream project, use its current documentation or repository page. Pin a tag or commit only when a statement depends on that specific version, and label the link accordingly.

## Common Sections

### Learning Objectives

```markdown
## Learning objectives

By the end of this tutorial, you will learn how to:
- Objective one.
- Objective two.
- Objective three.
```

### Prerequisites

```markdown
## Prerequisites

- Requirement one.
- Requirement two.
```

### UI procedure

```markdown
## Change a setting

1. Go to **Settings** > **Applications**.
2. Select the app and change the setting.
3. Click **Apply** and wait for the app to restart if required.
```

### Configuration Section

```markdown
## Configure the connection

1. Go to **Settings** > **Section**.
2. Enter the required value.

   :::tip
   Helpful tip about this configuration.
   :::
```

## Translation Guidelines

When translating between English and Chinese:

1. **Don't translate literally** — adapt the message
2. **Chinese is more concise** — shorter sentences, fewer words
3. **Keep technical terms consistent** — use established translations
4. **Maintain structure** — keep the same heading hierarchy
5. **Adapt examples** — use Chinese examples where appropriate

### Chinese use case delivery and reuse

For use cases, follow `use-case-writer` for English-first drafting and complete standalone Chinese delivery when in scope. Never substitute a whole English-page include for the Chinese page. Use matching localized reusable fragments where appropriate, checking their applicability, regions, and links.

## File Organization

```
docs/
├── use-cases/           # Tutorials (English)
│   ├── index.md
│   └── app-name.md
├── zh/
│   └── use-cases/       # Tutorials (Chinese)
│       ├── index.md
│       └── app-name.md
├── manual/              # User guides
│   ├── help/            # Troubleshooting (ts-*.md)
│   └── ...
├── developer/           # Developer documentation
│   ├── install/         # Installation guides
│   ├── concepts/        # Architecture concepts
│   ├── develop/         # App development
│   ├── reference/       # API references
│   └── contribute/      # Contribution guides
└── .vitepress/          # Navigation config
    ├── usecase.en.ts
    └── usecase.zh.ts
```

## Navigation Updates

For new use cases, follow `use-case-writer` for required sidebar and gallery entries. The language-specific sidebar entry shapes are shown below:

**For English** (`.vitepress/usecase.en.ts`):
```typescript
{
  text: "New App",
  link: "/use-cases/new-app",
}
```

**For Chinese** (`.vitepress/usecase.zh.ts`):
```typescript
{
  text: "新应用",
  link: "/zh/use-cases/new-app",
}
```

Update navigation for the language deliverables in scope. For use cases, follow the English-first bilingual workflow in `use-case-writer`. Most app names remain untranslated.

## Special Considerations

### Language-Specific Domain Differences

When writing documentation, use the appropriate domain for each language:

- **English documentation**: Use `https://www.olares.com` and `https://docs.olares.com`
- **Chinese documentation**: Use `https://www.olares.cn` and `https://docs.olares.cn`

Example:
```markdown
<!-- English -->
For more information, visit [Olares website](https://www.olares.com).

<!-- Chinese -->
更多信息请访问 [Olares 官网](https://www.olares.cn)。
```

### Specialized Skills

- **Use case tutorials** (in `/docs/use-cases/` or `/docs/zh/use-cases/`): Use `use-case-writer` instead. It handles drafts and engineering evidence, reader-task selection, required Learning objectives, content reuse, version metadata, and language deliverables.
- **UI strings and product copy**: Use `olares-ux-writing` for buttons, error messages, notifications, empty states, confirmation dialogs.

### Olares One Documentation

Olares One is a separate product line with its own documentation section (`/docs/one/`).

**Key differences from main Olares docs:**
- Target audience: Enterprise/business users
- Focus: Cloud deployment, team collaboration, admin features
- Tone: More formal, business-oriented
- Structure: May include admin consoles, team management, billing topics

**When writing Olares One docs:**
- Use business/enterprise terminology
- Include admin and team management workflows
- Cover deployment scenarios (cloud vs. on-premise)
- Address scalability and security concerns for organizations

File location: `/docs/one/` (English) and `/docs/zh/one/` (Chinese)

## Best Practices

1. **Always include a unique description** in frontmatter, under 160 characters
2. **Only override a long H1 with a frontmatter `title`** — otherwise omit it and let the H1 be the title
3. **Use outline to control TOC depth** — `[2, 3]` for most pages
4. **Add screenshots for UI steps** — use `#bordered` class
5. **Include alt text** for accessibility
6. **Test all links** before submitting
7. **Keep sentences short** — easier to read and translate
8. **Use active voice** — clearer and more direct
9. **Be consistent** with terminology across pages
10. **Use correct domains** — .com for English, .cn for Chinese
11. **Check for specialized skills** — `use-case-writer` for use cases, `olares-ux-writing` for UI copy
12. **Surface critical starting states** — State them before the action they affect. Use a top-of-page warning only when the consequence warrants it.
13. **Add useful checks after critical steps** — Tell readers what to observe when it determines whether they should continue, wait, or recover.

## References

- `references/document-types/troubleshooting.md` — Full Type 5 template, section guidelines, complex diagnostic flow
- `references/markdown-conventions.md` — VitePress frontmatter, admonitions, code blocks, lists, tables
- `references/developer-conventions.md` — Developer-doc-specific patterns (line-highlighted YAML, field tables, diagrams, cross-references)
- `references/examples/developer-architecture.md` — Architecture/concept doc sample
- `references/examples/developer-api.md` — API reference doc sample
