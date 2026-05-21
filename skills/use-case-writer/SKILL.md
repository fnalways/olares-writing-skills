---
name: use-case-writer
description: Transform Chinese drafts or inputs into polished English Olares documentation use cases. Each use case is a multi-file deliverable (English markdown, Chinese @include stub, EN sidebar entry, ZH sidebar entry), not a single markdown file. Use this skill when the user provides Chinese content about an application or workflow and wants it converted into the standard Olares use case format. Also trigger when the user mentions creating, writing, or rewriting use cases for the Olares docs site, especially for the docs/use-cases directory. This skill ensures consistent structure, terminology, and style matching existing Olares use cases. For long-form English documentation (manuals, developer docs, troubleshooting), see olares-docs-writer. For UI strings and product copy, see olares-ux-writing.
metadata:
  version: 0.2.0
---

# Olares Use Case Writer

Transform Chinese drafts into polished English use cases for the Olares documentation site.

## Purpose

This skill converts Chinese input (drafts, notes, or descriptions) into properly formatted, publication-ready English use case documentation that follows Olares' established conventions and style.

## Deliverables (all required for every new use case)

A complete task produces **four files**. The English markdown alone is NOT a complete deliverable. Do not stop after producing file 1.

1. `docs/use-cases/<app>.md` — the English use case.
2. `docs/zh/use-cases/<app>.md` — a one-line file containing `<!--@include: ../../use-cases/<app>.md-->`, so the Chinese site reuses the English content.
3. Updated `docs/.vitepress/usecase.en.ts` — new entry in the correct category and alphabetical position.
4. Updated `docs/.vitepress/usecase.zh.ts` — matching entry under the `/zh/use-cases/` link prefix.

If you skip files 2-4, the use case will not appear in the sidebar and will be invisible to readers. See Process step 6 below for exact placement rules.

## Output Format

Generate a complete Markdown file following this exact structure:

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
4. If the app is not yet published to Market (no `OlaresManifest.yaml` exists), use `"1.0.0"` as the default initial version.

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

### 2. Title (H1)
- Use action-oriented titles (start with a verb)
- Examples: "Deploy Stable Diffusion for AI image generation", "Stream games from your Olares device"

### 3. Introduction
- 1-2 short paragraphs. Structure with clear layers, not a flat list of features:
  - **Sentence 1**: What the app is (category + core technology)
  - **Sentence 2**: Core capabilities (input types, output types, key specs like language count)
  - **Sentence 3**: Additional capabilities or value on Olares
- Do NOT link app names to external sites (e.g., GitHub repositories). Use plain text for app names. The use case focuses on how to use the app within Olares, not on the upstream project.
- Avoid writing a "feature laundry list" where each sentence just adds another feature with no hierarchy
- Do NOT repeat the same information that appears in a summary table elsewhere in the doc
- **When a Learning objectives section follows**, do NOT add a "This guide shows you how to..." sentence that repeats the same list. The intro should describe the app and its value, not enumerate the steps covered.
- **CRITICAL: Do not fabricate descriptions for branded or proprietary apps.** When the app is a branded vendor product (e.g., NVIDIA NemoClaw, NVIDIA OpenShell), look up the official description from the vendor's product page (e.g., `build.nvidia.com/<product>`) before writing the intro. Do not guess what the acronym means, do not invent a backronym, and do not infer the product family from the name alone. If WebFetch times out, fall back to `curl -sL --max-time 30 <url>` and grep for the description.
- **Do not pull in unrelated cross-references.** If two apps happen to share a model, framework, or component, that does not warrant a "the same model used in [other-use-case]" sentence. Link only when the other doc is a true prerequisite or a directly relevant follow-up.

### 4. Learning Objectives (Optional)
Use only when the guide teaches multiple distinct skills. Skip for straightforward single-workflow guides.
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

The install section follows a **fixed two-step format**:

```markdown
## Install [App Name]

1. Open Market and search for "[App Name]".
   ![App Name](/images/manual/use-cases/app-name.png#bordered)

2. Click **Get**, then **Install**, and wait for installation to complete.
```

Rules:
- "Market" is an app name used standalone, so it is **not bolded**.
- Do not add a third step like "open the app from Launchpad".
- The second step always ends with "and wait for installation to complete".
- Step 1 should include a Market screenshot of the app below it (indented inside the step). If the screenshot file does not exist yet, use an HTML comment placeholder: `<!-- ![App Name](/images/manual/use-cases/app-name.png#bordered) -->`.
- **Capture install duration when the source provides one.** If the demo or input mentions an install time (e.g., "around 10 minutes"), include it in the install step with a network caveat: "Installation takes about 10 minutes, depending on your network." Do not invent a number when the source is silent.

#### Model name and endpoint acquisition

When a use case requires a local LLM endpoint (e.g., NemoClaw, Open WebUI, AnythingLLM connecting to Ollama or a model app), follow this exact flow. Do NOT swap the order or merge the two sources.

1. **Model name**: comes from the model app's Launchpad page, NOT from Settings.
   - Direct the user to open the model app from Launchpad and read the model name shown on the main page.
   - Reuse the existing model screenshot at `/images/one/<model>-downloaded.png` (e.g., `qwen3.5-27b-downloaded.png`). Check `openwebui.md` for the canonical reference before making a placeholder.

2. **Endpoint URL**: comes from Settings > Applications > [App] > Shared entrances (or Entrances for non-shared apps).
   - For shared apps, instruct the user to copy the URL from **Shared entrances**. Format is `http://{hash}.shared.olares.com`.
   - For non-shared apps, use **Entrances** > **Set up endpoint**.
   - Always direct users to obtain the endpoint from Settings rather than hardcoding URL templates.

Do NOT tell the user to find the model name in Settings, and do NOT tell the user to find the endpoint on the Launchpad page. The two pieces of info live in different places.

**Single-model app vs Ollama app**

| | Single-model app | Ollama app |
|:---|:---|:---|
| What it is | One app packages one specific model | One app hosts multiple models |
| Install from Market | Search the model name (e.g., `Qwen3.5 27B Q4_K_M (Ollama)`) | Search "Ollama" |
| Model download | Opens from Launchpad; download starts automatically | Open Ollama from Launchpad, then run `ollama pull <model>` |
| Model name source | Launchpad page displays it (e.g., `qwen3.5:27b-q4_K_M`) | `ollama list` or any model you have pulled |
| Endpoint source | Settings > Applications > **[Model App]** > Shared entrances | Settings > Applications > **Ollama** > Shared entrances |
| Endpoint selection | Select the model app name (or "Ollama API" if shown) | Select **Ollama API** |
| Endpoint format | `http://{hash}.shared.olares.com` | `http://{hash}.shared.olares.com` |
| Model ID for consumers | Exact model name shown on the app page | Any downloaded model ID (e.g., `qwen3.5:9b`) |

When writing a use case, **default to the single-model app flow** unless the source material explicitly uses Ollama. This avoids forcing the user to install an extra app and pull models manually.

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

When the use case involves a client app outside Olares (phone app, desktop app, browser on another computer) connecting to an Olares-hosted service, follow the patterns in `references/network-access-patterns.md`. It covers:

- When to use Tabs vs a Callout (connection-establishing sections vs configuration sections).
- The LAN tab template (`.local` domain, Windows users callout, URL conversion phrasing).
- The VPN tab template (authentication-level update, LarePass VPN screenshot reuse, per-field connection steps).
- The Callout pattern (default `.com` URL with `.local` tip).

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

```markdown
::: details Example: [specific description]
```text
[content]
```
:::
```

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
- Unsure whether a suitable screenshot exists → start with `<!-- -->`, then search `docs/public/images` and replace if found

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

### Voice and Tone
- Clear, direct, and natural. Write like you're explaining to a colleague, not drafting a formal specification.
- Second person ("you")
- Active voice
- Professional but conversational and approachable
- Avoid awkward dashes as sentence separators; use periods or restructure instead

### Writing for Readability

**Use simple, everyday words:**
| Avoid | Use |
|-------|-----|
| client device | computer |
| utilize | use |
| initiate | start |
| terminate | end |
| verify | check (unless verification is the specific action) |

**Be direct and action-oriented:**
- ❌ "You will need to slightly modify the URL you copied earlier"
- ✅ "Modify the URL slightly"

**Avoid filler phrases:**
- ❌ "In order to" → ✅ "To"
- ❌ "It is important to note that" → Remove or just state the fact
- ❌ "As mentioned previously" → Restate briefly or link
- ❌ "Please be advised that" → Just say it

**Write naturally:**
- ❌ "Based on whether X, the process is different"
- ✅ "The process depends on whether X"

**Focus on what the user achieves, not the mechanism:**
- ❌ "This guide will show you how to connect X to Y"
- ✅ "This guide shows you how to [achieve the goal] using X and Y"

**Prefer short, simple sentences over complex ones with multiple clauses.**

### Terminology Conventions
| Use | Avoid |
|-----|-------|
| Olares Market | Marketplace |
| Market (no bold when standalone) | **Market** (bold only in nav paths) |
| Launchpad | desktop |
| Settings | system settings |
| Control Hub | admin panel |
| LarePass VPN | VPN connection |
| Olares Files | Olares file system |
| Click **Button** | Click the button |
| Navigate to **Tab** | Go to the tab |

### Bolding rules

Bold only the following:
- **UI controls and labels in navigation paths**: `**Settings** > **Applications** > **[App]**`, `Click **Get**`, `**Authentication level**`.
- **Field names in configuration lists**: `- **VERSION:** Select your preferred version.`

Do NOT bold:
- App names used standalone (e.g., Files, Market, NemoClaw, OpenClaw). They are plain text.
- Inline emphasis like `**not**`, `**important**`. Use plain text or restructure the sentence.
- Hardware specs in Prerequisites (GPU, VRAM, CPU architecture).
- Cross-reference titles inside link labels. The link itself is the emphasis.

If you find yourself reaching for bold to add emphasis to a single word in prose, leave it plain. Bold is for UI affordances, not voice.

### App name references

**Market app names with qualifiers**
Single-model apps in Market often include a suffix such as `(Ollama)` in their display name (e.g., `Qwen3.5 27B Q4_K_M (Ollama)`).

- **First occurrence** in a use case: use the full Market name including the suffix.
- **Subsequent references**: you may shorten to the model name alone (e.g., `Qwen3.5 27B`).
- **In navigation paths** (Settings > Applications > ...): use the full name so the user can match it exactly in Settings.

**Do not fabricate app names.** If the source material mentions a model but you are unsure of its exact Market name, search existing use cases or leave a placeholder comment.

### Grammar Patterns
- Install steps: `"Click **Get**, then **Install**, and wait for installation to complete."`
- "Navigate to **Settings** > **Applications** > **[App]**"
- "Ensure [condition] before proceeding"
- "Wait for [process] to complete"
- Use "might" instead of "may" to express possibility (e.g., "This might take a few minutes")

### Common Phrases
- "Prerequisites" (not "Before you begin")
- "Learning objectives" (when applicable)
- "In this guide, you will learn how to:"

### Lists: Steps vs Configuration Fields vs Sub-steps

**Numbered steps (1. 2. 3.)**: Use for sequential actions that must be performed in order.

**CRITICAL: Do not insert non-list text (e.g., "Then, configure it in Jaaz:") between numbered steps.** This breaks the Markdown numbered list and causes step numbering to reset. If you need to group steps logically, either use a comment or keep all steps in a single continuous list.

**Unordered lists (-)**: Use ONLY for:
- Multiple configuration fields/options (no specific order required)
- Prerequisites or requirements
- Feature lists

**Nested sub-steps (a. b. c.)**: Use for sequential operations under a main step. Each sub-step must be on its own line with a blank line after.

**Examples:**

```markdown
<!-- Configuration fields - use unordered list -->
3. When prompted, set environment variables:
    - **VERSION:** Select your preferred version.
    - **DISK_SIZE:** Allocate disk space.

<!-- Operation steps - use sub-steps (a. b. c.) -->
3. Open VNC Viewer and create a new connection:

    a. Click **File** > **New Connection**.

    b. Enter the address and port number.

    c. Save the connection.
```

**Rule of thumb:**
- If it's **filling in configuration values**, use `-` (unordered)
- If it's **performing actions in sequence**, use `a. b. c.` (ordered sub-steps)

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

All images should include `#bordered` and be stored in `/images/manual/use-cases/`.

## Process

0. **Pre-writing checks** - Before writing the first sentence, gather facts that you cannot fabricate:

   **Endpoint patterns** - When a use case involves connecting Olares apps (e.g., Ollama, ComfyUI), do not fabricate endpoint URLs.
   - Search existing use cases (e.g., `grep "olares.com" docs/use-cases/`) to find the correct endpoint patterns.
   - Shared apps use **Shared entrances** in Olares Settings. The URL format is typically `http://{hash}.shared.olares.com`, NOT `https://{hash}.{username}.olares.com`.
   - Non-shared apps use **Entrances** > **Set up endpoint** in Olares Settings.
   - Always direct users to obtain the endpoint from **Settings** > **Applications** > **[App Name]** rather than hardcoding URL templates.

   **Brand and product descriptions for proprietary apps** - For any branded vendor product (e.g., NVIDIA NemoClaw, NVIDIA OpenShell, Cloudflare Workers), look up the official description from the vendor's product page before writing the intro. Do not guess what an acronym stands for or invent a backronym. If WebFetch times out, use `curl -sL --max-time 30 <url>` and grep the result.

   **Screenshot-only information** - When the source material places critical config values (env var names, endpoint formats, exact menu labels) only inside screenshots with no accompanying text, you must still produce actionable steps. Do not leave the user guessing. Apply this fallback:
   1. Write the most reasonable value based on Olares conventions and the surrounding context.
   2. Append an HTML comment immediately after the value: `<!-- FIXME: verify against source screenshot -->`.
   3. Flag it to the user during review so the screenshot can be checked.

   Example:
   ```markdown
   - **ANTHROPIC_MODEL**: Enter the model identifier from step 2. For example:
     ```plain
     qwen3.5:27b-q4_K_M
     ```
     <!-- FIXME: verify against source screenshot -->
   ```

1. **Analyze the Chinese input** - Identify:
   - The application/tool being documented
   - The main workflow or task
   - Prerequisites and dependencies (and which are already installed by the user, so link to those instead of writing a redundant install section)
   - Configuration requirements
   - Alternative paths or methods
   - Install duration if the source mentions one (capture verbatim, with a network caveat)
   - Hardware specs mentioned in source: distinguish "demo ran on this hardware" from "this is a hard requirement". Only the latter goes into Prerequisites.

2. **Structure the content** - Map the Chinese content to the standard use case sections

3. **Rewrite in English** - Following the style guidelines above

4. **Add formatting** - Insert appropriate Markdown elements (tips, tables, code blocks, tabs)

5. **Review** - Ensure:
   - All configuration values are specific and actionable
   - Commands are correct and complete
   - Links use relative paths for internal docs
   - Images follow naming conventions, and existing screenshots have been reused where available
   - Terminology matches Olares conventions
   - Bolding follows the rules in "Bolding rules" (no bold app names in plain prose, no bold `**not**` for emphasis)
   - Brand and product descriptions match the vendor's official wording (for branded apps)
   - No cross-references to unrelated use cases ("the same model used in [other-doc]")
   - Model name acquisition flow uses the Launchpad page; endpoint URL acquisition uses Settings > Shared entrances
   - **Frontmatter includes `app_version`, `doc_version`, `doc_updated`, and `head` keywords** (CRITICAL for new docs)

6. **Create remaining deliverables (REQUIRED, not optional)** - The English markdown file is only one of four required outputs. You MUST also create the Chinese stub and update both sidebar configs. Skipping this step makes the use case invisible on the docs site.

   **`docs/zh/use-cases/<app>.md`** (REQUIRED) - Create the Chinese version using `@include` to reuse the English content:
   ```markdown
   <!--@include: ../../use-cases/<app>.md-->
   ```
   This is a single line. The Chinese file inherits the full English doc including frontmatter.

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

   **`docs/.vitepress/usecase.zh.ts`** (REQUIRED) - Add to Chinese sidebar navigation with the same placement. Use the app name as-is (most app names are not translated). Link prefix is `/zh/use-cases/`.

   **`docs/use-cases/index.md`** (CONDITIONAL) - Add to "Featured use cases" section only if it's one of the core/essential guides (currently: ComfyUI, OpenClaw, Windows, Steam). Otherwise, it will only appear in the sidebar navigation.

7. **Verify all deliverables exist** - Before reporting completion, confirm that all four required files have been created or updated:
   - [ ] `docs/use-cases/<app>.md` exists
   - [ ] `docs/zh/use-cases/<app>.md` exists with the one-line `@include`
   - [ ] `docs/.vitepress/usecase.en.ts` contains the new entry
   - [ ] `docs/.vitepress/usecase.zh.ts` contains the new entry

   If any file is missing, the task is incomplete. Do not tell the user the use case is ready until all four are in place.

8. **Output** - Provide a short summary listing the four files you created or modified, so the user can spot-check.

## Example Transformation

For a sample showing how a Chinese input becomes a polished English use case (frontmatter, intro, prerequisites, install steps, and tips), see `references/example-transformation.md`.
