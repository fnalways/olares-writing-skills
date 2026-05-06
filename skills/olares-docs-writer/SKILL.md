---
name: olares-docs-writer
description: Write Olares documentation in English and Chinese for the VitePress docs site. Use when the user wants to create or edit manuals, developer docs, troubleshooting guides, FAQ entries, or translations between English and Chinese, and when they mention `docs.olares.com`, `docs/manual/`, `docs/developer/`, or `docs/manual/help/`. Enforces the Olares style guide and VitePress conventions. For Chinese-to-English use case tutorials, use use-case-writer instead. For UI strings and product copy, see olares-ux-writing.
metadata:
  version: 0.1.0
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

Step-by-step guides for specific applications or workflows.

**Structure:**
1. Frontmatter with `outline` and `description`
2. Main title (`#`) — descriptive and actionable
3. Introduction paragraph — what this guide covers
4. Learning objectives — bullet list of what users will learn
5. Prerequisites — what users need before starting
6. Step-by-step instructions — numbered lists with clear actions
7. Tips and info boxes (`:::tip`, `:::info`)
8. FAQ section (optional)

**Example frontmatter:**
```yaml
---
outline: [2, 3]
description: Step-by-step guide to installing ACE-Step AI on Olares...
---
```

For Chinese-to-English use case work, use the dedicated `use-case-writer` skill. For a complete English+Chinese sample, see `references/examples/use-case-en.md` and `references/examples/use-case-zh.md`.

### 2. Manual/Guide Documentation

Feature explanations and user guides.

**Structure:**
1. Frontmatter with `description`
2. Main title
3. Concept explanation
4. Feature overview
5. How-to sections
6. Configuration details

### 3. Index Pages

Use `FilterableList` component for use cases index:

```yaml
---
description: Explore practical use cases of Olares...
---
# Use cases

Intro paragraph...

<FilterableList :items="[
  { title: 'App Name', link: './app-file.html', tags: ['AI'] },
]" />
```

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

## Markdown Conventions

For VitePress markdown syntax (frontmatter, headings, admonitions, images, icons, code blocks, lists, tables, links), see `references/markdown-conventions.md`.

Two Olares-specific rules to keep in mind:

- **Bullet labels with bold**: Use bold only when a label acts as a category header (`- **Hardware**: ...`). Do NOT bold for emphasis in body text or in admonition labels (`**Verify changes:**` inside a warning).
- **Frontmatter required fields**: Every page needs `description`. Most pages also need `outline: [2, 3]`.

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

### Installation Steps

```markdown
## Install AppName

1. Open the **Market** app in your Olares web interface.
2. Search for "AppName".
3. Click **Get**, then click **Install**.
   ![Installation screenshot](../public/images/manual/use-cases/filename.png#bordered)
4. Wait for the installation to complete.
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

### Chinese doc reuse via @include

Most Chinese use case docs reuse the English content directly via VitePress `@include`. Instead of translating the entire file, create a one-line Chinese file:

```markdown
<!--@include: ../../use-cases/<app>.md-->
```

This inherits the full English doc including frontmatter. Only create a standalone Chinese translation when the content needs significant localization.

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

After creating a new doc, update **both** sidebar configs:

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

Always update both files together. Most app names are not translated in the Chinese sidebar (e.g., "ComfyUI", "Ollama", "Jaaz" stay as-is).

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

- **Use case tutorials** (in `/docs/use-cases/` or `/docs/zh/use-cases/`): Use `use-case-writer` instead. It handles Chinese-to-English transformation, frontmatter `app_version`/`doc_version`/`doc_updated` fields, and the install-section / endpoint-acquisition / network-access patterns.
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

1. **Always include a description** in frontmatter for SEO
2. **Use outline to control TOC depth** — `[2, 3]` for most pages
3. **Add screenshots for UI steps** — use `#bordered` class
4. **Include alt text** for accessibility
5. **Test all links** before submitting
6. **Keep sentences short** — easier to read and translate
7. **Use active voice** — clearer and more direct
8. **Be consistent** with terminology across pages
9. **Use correct domains** — .com for English, .cn for Chinese
10. **Check for specialized skills** — `use-case-writer` for use cases, `olares-ux-writing` for UI copy

## References

- `references/document-types/troubleshooting.md` — Full Type 5 template, section guidelines, complex diagnostic flow
- `references/markdown-conventions.md` — VitePress frontmatter, admonitions, code blocks, lists, tables
- `references/developer-conventions.md` — Developer-doc-specific patterns (line-highlighted YAML, field tables, diagrams, cross-references)
- `references/examples/use-case-en.md` — Complete English use case sample
- `references/examples/use-case-zh.md` — Complete Chinese use case sample
- `references/examples/developer-architecture.md` — Architecture/concept doc sample
- `references/examples/developer-api.md` — API reference doc sample
