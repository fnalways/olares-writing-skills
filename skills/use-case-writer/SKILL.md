---
name: use-case-writer
description: Create and revise bilingual Olares use case tutorials from Chinese or English drafts, app-porting notes, test results, implementation context, or existing PRs. Use when writing or editing app walkthroughs under docs/use-cases. Organize supported facts around a useful reader task and reuse applicable documentation. Produce English deliverables first and complete Chinese deliverables after English finalization. For manuals, developer references, or troubleshooting-only pages, see olares-docs-writer. For UI copy, see olares-ux-writing.

metadata:
  version: 0.6.0
---

# Olares Use Case Writer

Turn source material into English and Chinese tutorials that help readers complete useful tasks on Olares.

## Purpose

Accept drafts, porting notes, test logs, screenshots, implementation changes, and existing PRs as evidence. Determine the reader and task before choosing an outline. A developer author does not make developers the target audience.

Before drafting or reviewing, read [Tutorials from evidence](references/tutorial-from-evidence.md) for content selection and reuse, and [Writing style](references/writing-style.md) for prose conventions.

## Deliverables

A new use case requires the English page and two discovery updates below. For revisions, update affected existing entries without duplicating them.

Keep deliverables within the requested scope. Test notes do not automatically require public acceptance-test pages. Put execution records in the PR or an existing internal test record. Create a reader-facing validation or diagnostic guide only when requested.

### Required for every new use case (English-first)

1. `docs/use-cases/<app>.md`: the English use case.
2. Updated `docs/.vitepress/usecase.en.ts`: new entry in the correct category and alphabetical position.
3. Updated `docs/.vitepress/data/useCases.ts`: new entry so the use case appears in the filterable gallery on the Use cases index page.

If you skip files 2-3, the use case will not appear in the sidebar or the gallery and will be invisible to readers.

### Created after English is finalized (Chinese)

4. `docs/zh/use-cases/<app>.md`: a complete standalone Chinese translation with localized frontmatter, the AI-translation warning, and natural Chinese copy.
5. Updated `docs/.vitepress/usecase.zh.ts`: matching entry under the `/zh/use-cases/` link prefix.

Do not create the Chinese page while the English copy is still changing. Once the user confirms the English version is finalized, create the complete Chinese translation automatically. Never use a whole-page `@include` stub as the Chinese deliverable. Localized reusable fragments may still be included from `docs/zh/reusables/` when both languages have matching reusable files.

## Output Format

Use the following structure. Include Learning objectives in every use case. Adapt the main workflow headings and number of steps to the actual task.

### 1. Frontmatter (YAML)

**CRITICAL: All new use cases MUST include these fields:**

```yaml
---
outline: [2, 3]
description: [Concise SEO-friendly summary, 1-2 sentences]
head:
  - - meta
    - name: keywords
      content: [keyword1, keyword2, keyword3, ...]  # SEO keywords
app_version: "X.Y.Z"      # REQUIRED: Current app version from OlaresManifest.yaml
doc_version: "1.0"        # REQUIRED: Doc version (1.0=initial, 1.1=minor update, 2.0=major rewrite)
doc_updated: "YYYY-MM-DD" # REQUIRED: Today's date in YYYY-MM-DD format
---
```

**Field requirements:**

| Field | Required | Value Source |
|-------|----------|--------------|
| `outline` | Yes | Use `outline: deep` or `outline: [2, 3]` depending on TOC depth needed |
| `description` | Yes | SEO-friendly summary (1-2 sentences) |
| `head` | Yes | Meta keywords for SEO. Format: `content: "Olares, app-name, category, keywords"` |
| `app_version` | **Yes** | Get from `OlaresManifest.yaml` → `metadata.version` |
| `doc_version` | **Yes** | Start with `"1.0"`. Increment: `1.1` for minor updates, `2.0` for major rewrites |
| `doc_updated` | **Yes** | Current date in YYYY-MM-DD format |

**How to get `app_version`:**
1. Find the app's `OlaresManifest.yaml` file
2. Look for `metadata.version` field
3. Copy the exact version string (e.g., `"1.0.8"`)
4. If the manifest is unavailable, obtain a traceable package version from the release source or author. Do not invent `"1.0.0"`. Identify a missing version as unresolved in the draft and review summary before publication.

Example:
```yaml
# From OlaresManifest.yaml:
metadata:
  version: '1.0.8'  # ← Use this value

# In your use case frontmatter:
app_version: "1.0.8"
```

**`doc_version` versioning guide:**
- `"1.0"` - Initial release
- `"1.1"` - Minor updates (typos, new screenshots, small clarifications)
- `"1.2"` - Additional content or sections added
- `"2.0"` - Major rewrite, workflow changes, UI overhaul
- `"2.1"` - Minor updates to the 2.0 version

**Keywords guidelines:**
Include in `head.meta.content`:
- `Olares` (always)
- App name (e.g., `Stable Diffusion`, `n8n`)
- Category (e.g., `AI`, `automation`, `game streaming`)
- Key features (e.g., `self-hosted`, `workflow`, `image generation`)

**Content length: quality over arbitrary thresholds**

Do not pad text, add filler sections, or inflate descriptions just because an SEO plugin flags a page as "too short." Use case length should be determined by the workflow's actual complexity and what the user needs to succeed.

- A simple single-app guide should stay short.
- A complex multi-app workflow deserves the space it needs.
- If a plugin reports thin content, first check whether steps are missing or unclear, not whether the word count is high enough.

### 2. Title (H1)
- Use action-oriented titles (start with a verb)
- Examples: "Deploy Stable Diffusion for AI image generation", "Stream games from your Olares device"
- **Check for duplicate H1 titles before finalizing.** Search existing docs with:
  ```bash
  find docs -type f -name '*.md' -not -path '*/node_modules/*' | xargs grep -h '^# ' | sort | uniq -d
  ```
  If the title already exists, make it more specific by adding the app name, product area, or scenario. For example, prefer "Open WebUI common issues" over "Common issues".

### 3. Introduction
- 1-2 short paragraphs. Structure with clear layers, not a flat list of features:
  - **Sentence 1**: What the app is (category + core technology)
  - **Sentence 2**: Core capabilities (input types, output types, key specs like language count)
  - **Sentence 3**: Additional capabilities or value on Olares
- Do NOT link app names to external sites (e.g., GitHub repositories). Use plain text for app names. The use case focuses on how to use the app within Olares, not on the upstream project.
- Avoid writing a "feature laundry list" where each sentence just adds another feature with no hierarchy
- Do NOT repeat the same information that appears in a summary table elsewhere in the doc
- **Learning objectives follows the introduction.** Do NOT add a "This guide shows you how to..." sentence that repeats the same list. The intro should describe the app and its value, not enumerate the steps covered.
- **CRITICAL: Do not fabricate descriptions for branded or proprietary apps.** When the app is a branded vendor product (e.g., NVIDIA NemoClaw, NVIDIA OpenShell), look up the official description from the vendor's product page (e.g., `build.nvidia.com/<product>`) before writing the intro. Do not guess what the acronym means, do not invent a backronym, and do not infer the product family from the name alone. If WebFetch times out, fall back to `curl -sL --max-time 30 <url>` and grep for the description.
- **Do not pull in unrelated cross-references.** If two apps happen to share a model, framework, or component, that does not warrant a "the same model used in [other-use-case]" sentence. Link only when the other doc is a true prerequisite or a directly relevant follow-up.

### 4. Learning Objectives (Required)
Include this section in every use case, including a short single-workflow guide. Use a brief list of concrete outcomes the reader will achieve. Keep it distinct from the introduction and avoid test-coverage goals. Use `学习目标` in Chinese.
```markdown
## Learning objectives
In this guide, you will learn how to:
- [Specific skill 1]
- [Specific skill 2]
```

### 5. Prerequisites (Optional)
Include only when there are real dependencies (e.g., another app must be installed first, specific hardware required). Skip if the only prerequisite is "Olares installed and running".

Do **not** bold hardware or spec mentions (GPU, CPU architecture, VRAM, etc.) in Prerequisites. Write them as plain text.

**When the user says a dependency is already installed, do NOT write an install section for it.** List it as a prerequisite with a link to its own use case (e.g., `[Local model app installed](openwebui.md)`) and move on. Don't bundle a second install walkthrough for the dependency into the new use case.

**Don't invent hardware constraints.** Do not add minimum GPU VRAM, CPU core count, or RAM requirements unless the source material explicitly states them as hard requirements. A demo running on specific hardware is not the same as that hardware being a requirement.

**Do not use conditional prerequisites.** Never write "if you plan to use..." or "when using..." in Prerequisites. Instead:
- Pick one primary example and declare it in the intro (e.g., "This guide uses a single-model app as an example").
- Move optional requirements into the relevant subsection.

```markdown
## Prerequisites
- [Required app/installation] with link to its use case if exists
- [Configuration requirement]
- [Account requirement]
```

### 6. Main Content Sections

#### Installation section

Use this standard pattern when installation requires no additional input:

```markdown
## Install [App Name]

1. Open Market and search for "[App Name]".
2. Click **Get**, then **Install**, and wait for installation to complete.
```

- Keep standalone Market unbolded. Search for a matching existing screenshot before adding an indented image or comment placeholder.
- If installation prompts for a password, service URL, or configuration, explain where to obtain it and add the actions in their actual UI order, including confirmation. There is no fixed step count. Use a field table or unordered list for parallel settings.
- Put first-run initialization after installation. If an installed app's service or guest OS is not ready yet, keep the observable readiness step before connecting.
- Include a duration only when supported and useful for planning. Label environment-dependent estimates. A single test-run time does not establish typical installation time.

#### Model name and endpoint acquisition

When connecting models or app APIs, read [Connection sources](references/connection-sources.md). Identify Router, a direct model service, or an app API before choosing identifiers and endpoints. Use the current repository's canonical guide and applicable reusable regions. Do not apply the Launchpad model-name rule to Router identifiers.

#### Feature sections

Organize by logical workflow phases:
- `## Configure [Feature]` - Setup steps
- `## Use [App Name]` - How to use

When an app has **multiple parallel features or modes** (e.g., different tabs for different tasks), group them under a single H2 (e.g., `## Use [App Name]`) with each feature as an H3. Do NOT make each feature a separate H2.

Use H3 (`###`) for sub-steps within each section.

**Avoid orphan H3 headings**: If an H2 section would contain only a single H3, remove the H3 and place its content directly under the H2. A lone H3 adds unnecessary nesting.

### 7. Special Elements

#### Tips
```markdown
:::tip [Title]
Helpful information that makes the task easier
:::
```

#### Comparison Tips (for access methods)
When comparing browser-based access vs. client access, clearly distinguish:
- **Browser**: No installation, immediate access, suitable for quick tasks
- **Client app**: Better performance, full features (clipboard, file transfer, audio), better for extended use

Example:
```markdown
:::tip Browser vs. VNC Client
- **Browser access**: Requires no additional software. Best for quick tasks and initial setup.
- **VNC Client**: Provides better performance, bi-directional clipboard sharing, and persistent connections. Recommended for daily use.
:::
```

#### Information
```markdown
:::info
Important context or note
:::
```

#### Warnings
```markdown
:::warning
Critical caution about data loss or security
:::
```

#### Tabs (for alternative methods)
```markdown
<tabs>
<template #Tab-Label-1>
Content for method 1
</template>
<template #Tab-Label-2>
Content for method 2
</template>
</tabs>
```

#### Network access for external clients (LAN vs VPN)

When the use case involves a client app outside Olares (phone app, desktop app, browser on another computer) connecting to an Olares-hosted service, follow the patterns in `references/network-access-patterns.md`. It covers protocol and access-path selection, current canonical instructions, reuse, and choosing headings, tabs, or callouts without repeating the same connection details.

#### Tables (for configuration values)
```markdown
| Settings | Value | Description |
|:---------|:------|:------------|
| Field 1  | Value | What it does |
```

#### Code Blocks
- Use `bash` for terminal commands
- Use `json` for configuration
- Use `text` for plain text examples

**Long examples and prompts**
When including a long code block, prompt, or transcript that exceeds 20 lines, collapse it with a `details` container so it does not dominate the page:

````markdown
::: details Example: [specific description]
```text
[content]
```
:::
````

The title must be specific (e.g., `Example: mini BFF prompt`), not generic (`Example prompt`).

#### Images
Use this format for screenshots:
```markdown
![Alt text](/images/manual/use-cases/[filename].png#bordered)
```
Optional: Add `{width=XX%}` for sizing.

When screenshots are not yet available, use HTML comments as placeholders so the doc can be previewed without broken images:
```markdown
<!-- ![Alt text](/images/manual/use-cases/[filename].png#bordered) -->
```

**CRITICAL: Do not place image placeholders (HTML comments) between numbered list steps.** This breaks Markdown list numbering. Instead, either indent the placeholder inside a step or move all placeholders to the end of the step list.

**Reuse existing screenshots** when available. Do not placeholder a screenshot before checking these locations:
- LarePass VPN: `/images/manual/get-started/larepass-vpn-mobile.png`, `larepass-vpn-desktop.png`.
- Model app screenshots (Qwen, Gemma, Ollama): `/images/one/<model>.png`, `<model>-downloading.png`, `<model>-downloaded.png`. Check `openwebui.md` for the canonical reference.
- Shared entrance / endpoint screenshots: search existing use cases (e.g., `deerflow2-shared-entrance.png`) before creating new ones.

**Common reusable screenshot quick reference**

| Screenshot | Path | Notes |
|:---|:---|:---|
| Model name on Launchpad (27B) | `/images/manual/use-cases/deerflow2-get-model-name.png` | Shows `qwen3.5:27b-q4_K_M`. Do not use for 9B models. |
| Model name on Launchpad (9B) | `/images/manual/use-cases/litellm-model-name.png` | Shows `qwen3.5:9b`. Do not use for 27B models. |
| Shared entrance (generic) | `/images/manual/use-cases/ollama-shared.png` | Settings > Shared entrances page. Works for both Ollama and single-model apps. |
| LarePass VPN desktop | `/images/manual/get-started/larepass-vpn-desktop.png` | Generic, reusable across use cases. |
| Model downloading | `/images/one/<model>-downloading.png` | e.g., `qwen3.5-27b-downloading.png` |
| Model downloaded | `/images/one/<model>-downloaded.png` | e.g., `qwen3.5-27b-downloaded.png` |

**Screenshot placeholder decision tree**
- Need a new screenshot and will capture it later → `<!-- ![...] -->`
- Existing screenshot covers the same UI state → use the existing path directly
- Unsure whether a suitable screenshot exists → search `docs/public/images` and nearby guides first, then use a comment placeholder only if none fits

Only use placeholders for screenshots that genuinely do not yet exist.

### 8. FAQ Section (if applicable)
```markdown
## FAQs

### [Question]
[Answer]

#### Cause
[Explanation of why it happens]

#### Solution
[How to fix it]
```

### 9. Learn More
```markdown
## Learn more
- [Related use case 1](related1.md): Brief description.
- [Related use case 2](related2.md): Brief description.
```

Use "Learn more" as the standard heading (not "Next steps"). Format all items as links with a brief description. Do not mix plain-text bullets with link bullets.

## Style Guidelines

Read [Writing style](references/writing-style.md) before drafting or reviewing. It defines punctuation, tutorial voice, terminology, bolding, and list conventions.
- Do not use dashes to introduce explanations, insert asides, or join clauses. Range notation such as `12–128 characters` is allowed.
- Do not use English or Chinese semicolons in authored prose. Preserve required syntax in code, commands, URLs, and exact UI labels.
- Write a task-oriented tutorial. Keep useful success signals, but avoid test-report narration, fixed-answer assertions, repeated caveats, and irrelevant implementation details.

## Image Naming Conventions

**Installation screenshots**: Use the app name directly, without an `-install` suffix:
```
whisper-webui.png
ollama.png
```

**Other screenshots**: Follow the pattern `[app-name]-[action]-[detail].png`:
```
dify-create-app.png
ollama-authentication-level.png
openclaw-persona-files.png
```

New use case screenshots belong in `/images/manual/use-cases/` and use `#bordered`. Reuse matching screenshots in other existing directories without copying them.

## Process

0. **Extract supported facts**. Read the source material and current app configuration. Check critical UI labels and screenshot-only values against the screenshot or a reliable source. Do not guess a value and hide the uncertainty in a FIXME. Track missing facts in the draft and review summary. Verify branded product descriptions with the vendor's official source.

1. **Choose the reader task and sort the evidence** using `references/tutorial-from-evidence.md`. Separate required actions, useful readiness checks, known user-facing limits, optional configuration, and engineering validation records. Distinguish demo hardware from real requirements.

2. **Search for reuse before drafting**. Inspect `docs/reusables/`, localized fragments, canonical guides, and existing screenshots. Verify region names and applicability. Include required inline procedures, link separate prerequisites, and write app-specific differences locally.

3. **Design a coherent example**. Select one useful outcome and a clear default path. Explain how readers can substitute their own data. Do not invent unsupported features, hard requirements, or successful test results.

4. **Write the English tutorial**. Include Learning objectives. Explain where required values come from and where commands run. Place optional configuration after the main workflow. Use headings, tables, lists, and tabs only where they clarify the task.

5. **Review content and accuracy** with the final-review criteria in `references/tutorial-from-evidence.md` and the style reference. Preserve useful checks and known limits. Confirm model and endpoint sources match the connection type, and all required frontmatter is supported.

6. **Create required English deliverables (REQUIRED, not optional)** - The English markdown file is only one of three required outputs. You MUST also update the English sidebar and the gallery data file. Skipping this step makes the use case invisible on the docs site.

   **`docs/.vitepress/usecase.en.ts`** (REQUIRED) - Add to English sidebar navigation:
   - Each category is a **top-level section** (not nested under "Use cases")
   - Use **sentence-case** for category names: "Virtual machine", "Entertainment", "Productivity"
   - Insert under the appropriate category section
   - Within each category, maintain **alphabetical order**
   - Section order: AI → Virtual machine → Entertainment → Productivity → Social

   **AI category ordering guide** - The AI section is not strictly alphabetical. It follows a rough grouping:
   1. **Major agent/chat apps with sub-pages** (OpenClaw, Hermes Agent, OpenCode, Open WebUI, ComfyUI, NemoClaw)
   2. **Tool-type AI apps** (Context7, Ollama, Open Notebook)
   3. **Remaining AI apps in alphabetical order** (ACE-Step → AnythingLLM → Bifrost → Claude Code → ...)
   Place new AI use cases in the correct alphabetical position within group 3, or in group 1/2 if the app clearly belongs there.

   **`docs/.vitepress/data/useCases.ts`** (REQUIRED) - Add an entry to the `useCases` array so the app appears in the filterable gallery on the Use cases index page (`docs/use-cases/index.md`). The index page renders this array via the `UseCaseGallery` component. It does not list individual use cases itself, so a missing entry means the app is absent from the index. The gallery is locale-aware (it reads `lang` from VitePress and switches between English and Chinese), so each entry can carry both languages.
   - Entry format: `{ title: "<App name>", link: "/use-cases/<app>", category: "<Category>", description: "<short EN one-liner>", descriptionZh: "<short ZH one-liner>" },`
   - `title` (required): the app name as shown in the sidebar (e.g., `OpenClaw`, `Open WebUI`). Most app names are not translated, so `titleZh` is usually unnecessary. Add the optional `titleZh` only when the app has a real Chinese name (e.g., a built-in app like `文件管理器`).
   - `link` (required): the site-absolute path `/use-cases/<app>` (no `.md`, no leading `./`).
   - `category` (required): must match one of the categories in the `useCaseCategories` array exactly (`AI agent`, `AI workbench`, `Creative media`, `Model services`, `Embodied AI`, `Virtual machine`, `Entertainment`, `Productivity`, `Developer tools`, `Utilities`). Place the entry inside that category's block in the array. `category` is the canonical English key. Do NOT translate it here. The gallery localizes pill labels via the separate `categoryLabelsZh` map. If the use case needs a brand-new category, add it to BOTH `useCaseCategories` (English order) and `categoryLabelsZh` (Chinese label) before using it.
   - `description` (required): a short, punchy English gallery blurb (about 5-12 words), no trailing period. This is NOT the long SEO `description` from the page frontmatter. Write a concise one-liner.
   - `descriptionZh` (recommended): the Chinese gallery blurb, no trailing period. If omitted, the gallery falls back to the English `description` on the Chinese site, so add it whenever you have the Chinese copy.
   - When **deleting** a use case, remove its entry from this array too, or it will leave a dead card.

7. **Create complete Chinese deliverables after English finalization** - If it is unclear whether the English version is final, ask the user once. Do not ask whether they want an `@include` stub or a full translation; whole-page stubs are obsolete.

   - **If the English version is not finalized or the user does not confirm**, skip the Chinese page and ZH sidebar entry. Tell the user they will be added after English finalization.
   - **If the user confirms the English version is finalized**, automatically create both Chinese deliverables:
     - Translate the full page into natural Chinese. Do not translate sentence by sentence mechanically.
     - Localize the frontmatter `description` and keywords. Keep `app_version`, `doc_version`, and `doc_updated` aligned with the English page.
     - Add this warning after the frontmatter:

       ```markdown
       :::warning
       本文档由 AI 自动翻译，仅供参考。涉及关键操作或信息时，请以[英文原文](../../use-cases/<app>.md)为准。
       :::
       ```

     - Preserve the English heading structure, code, commands, and exact UI labels where the product UI is not localized.
     - Localize internal links to `/zh/` counterparts when they exist.
     - Reuse matching fragments from `docs/zh/reusables/` when appropriate. Never include the whole English page.
     - Add the matching entry to `docs/.vitepress/usecase.zh.ts`.

8. **Review the final state and verify deliverables**. After the last content change, apply the final-review criteria in `references/tutorial-from-evidence.md` to the affected English and Chinese pages, metadata, gallery text, and applicable included fragments. Repeat after technical follow-ups or FAQ additions. Then confirm:
   - [ ] `docs/use-cases/<app>.md` exists and includes Learning objectives
   - [ ] `docs/.vitepress/usecase.en.ts` contains the new entry
   - [ ] `docs/.vitepress/data/useCases.ts` contains the new gallery entry
   - [ ] (If English finalized) `docs/zh/use-cases/<app>.md` contains a complete Chinese translation with 学习目标, not a whole-page `@include`
   - [ ] (If English finalized) `docs/.vitepress/usecase.zh.ts` contains the new entry

   If any required file is missing, the task is incomplete. Do not tell the user the use case is ready until all required items are in place.

9. **Output** - Provide a short summary listing the files you created or modified. If English is not finalized, state that the Chinese page and navigation are pending finalization.

## Example Transformation

For examples of turning source notes into reader tasks, including required Learning objectives and retained readiness checks, see `references/example-transformation.md`. These are editorial examples, not current product specifications.
