# Markdown conventions (VitePress)

VitePress-specific Markdown patterns for Olares docs.

## Frontmatter

```yaml
---
title: Short title override   # Optional; ONLY when the H1 is too long. Omit it otherwise — the H1 is used automatically
outline: [2, 3]               # Table of contents depth
description: ...              # SEO description (required, unique, under 160 characters)
noindex: true                 # Optional; keep this page out of search engines (fragments, outdated, orphans)
head:                         # Optional meta tags
  - - meta
    - name: keywords
      content: Olares, ...
---
```

Notes:
- `title` overrides only the `<title>` tag, not the visible H1. Add it **only** when the H1 is too long; otherwise omit it and the H1 is used automatically.
- `search: false` removes a page from on-site search only; it does **not** deindex it from Google. Use `noindex: true` for that.
- Quote a `description`/`content` value only when it contains YAML-special characters (a colon-space, or a leading `>`, `|`, `#`, `&`, `*`, `[`, `{`, `"`, `'`).
- See the "SEO metadata guidelines" section in `SKILL.md` for full guidance.

## Headings

- `#` - Page title (only one per page)
- `##` - Major sections
- `###` - Subsections
- `####` - Sub-subsections (rare)

## Admonitions (callouts)

```markdown
:::tip Title
Helpful suggestion or recommendation
:::

:::info Title
Neutral information
:::

:::warning Title
Caution or important notice
:::

:::danger Title
Critical warning
:::
```

## Images

```markdown
![Alt text](../public/images/manual/use-cases/filename.png#bordered)

![Alt text](../public/images/manual/use-cases/filename.png#bordered){width=60%}
```

## Icons

Use Material Design Icons:

```markdown
<i class="material-symbols-outlined">settings</i>
<i class="material-symbols-outlined">more_horiz</i>
<i class="material-symbols-outlined">download</i>
```

## Code blocks

```markdown
```bash
# Shell commands
```

```yaml
# YAML with line highlighting
env:
  - name: CLI_ARGS
```

```plain
# Plain text output or logs
```
```

## Lists

**Ordered lists for steps:**
```markdown
1. First action.
2. Second action.

   Additional explanation for step 2.

3. Third action.
```

**Unordered lists for features:**
```markdown
- Feature one
- Feature two
- Feature three
```

**Bullet labels with bold:**
Use bold for bullet labels when they act as category headers:
```markdown
- **Hardware**: List of hardware requirements
- **Software**: List of software requirements
- **Local play**: Description of local play mode
```

Do NOT use bold for:
- General emphasis in body text (restructure the sentence instead)
- Labels in admonitions (e.g., avoid `**Verify changes:**` in warning callouts)

## Tables

```markdown
| Column 1 | Column 2 |
|----------|----------|
| Value 1  | Value 2  |
```

## Links

```markdown
[Link text](./relative-path.md)
[Link text](/absolute/path.md)
```
