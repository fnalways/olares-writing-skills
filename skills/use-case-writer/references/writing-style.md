# Use case writing style

### Voice and Tone
- Clear, direct, and natural. Write like you're explaining to a colleague, not drafting a formal specification.
- Second person ("you")
- Active voice
- Professional but conversational and approachable
- Follow the punctuation and tutorial voice rules below in both English and Chinese.

### Punctuation

- Do not use dashes to introduce explanations, append comments, insert parenthetical remarks, or join clauses. This includes em dashes, en dashes used as sentence punctuation, Chinese double dashes, and spaced hyphens used as substitutes. Use a period, a colon, or a rewritten sentence.
- En dashes that express ranges are correct and allowed, such as `12–128 characters` and `12–128 个字符`. Keep ordinary hyphens in compound words and technical names.
- Do not use English or Chinese semicolons in authored prose. Split the sentence or restructure it.
- Apply these rules to headings, introductions, steps, tables, callouts, metadata descriptions, and gallery blurbs. Preserve required syntax in code, commands, URLs, and exact UI labels.
- During review, inspect dash and semicolon matches in context. Do not reject a numeric range or blindly replace punctuation in technical literals.

### Tutorial voice

Write around a useful task the reader wants to complete. Use test notes and demo results as evidence for the instructions, then rewrite them as a tutorial.

- Organize the main flow around the reader's actions and results. Do not organize it around test cases, assertions, pass/fail checks, or a record of what the author validated.
- Use realistic, small examples that teach the workflow. A sample answer can illustrate the result, but do not require an exact wording match or turn each step into an acceptance test.
- Keep checks that help the reader proceed or recover. For a wait or readiness check, give a verified, observable signal and where to find it. Do not invent a status label or remove a necessary check just to make the prose lighter.
- Keep implementation details only when they help the reader choose a setting, understand a constraint, or resolve a problem. Move build validation, architecture test coverage, and evidence limitations to the review or PR description. Keep actual compatibility requirements in the guide.
- Explain a caveat once, near the relevant action. Avoid repeated credential distinctions, generic accuracy disclaimers, and statements about what an operation does not prove unless they prevent a concrete mistake.
- Include advanced alternatives only with usable instructions or a directly relevant link. Do not interrupt a basic workflow with an unexplained model, vector dimension, or internal component.

Examples:

| Test-report wording | Tutorial wording |
| --- | --- |
| Check that the answer identifies Suzhou and Dr. Chen. | Ask where the laboratory is located and who directs it. Open a source link to read the passage used in the answer. |
| The ingestion view shows how documents connect to flows and storage. | Select the uploaded document and submit it to a flow for processing. |
| Begin with the short TXT example to distinguish parsing delays from model connection problems. | For your first document, use a short TXT file. PDF and DOCX files can take longer to process the first time. |

Use the last example only when the delay is supported by the app's behavior or source material. Do not copy these examples as universal product claims.

For content selection, required Learning objectives, reuse, and review after technical follow-ups, see [Tutorials from evidence](tutorial-from-evidence.md). [Example transformation](example-transformation.md) shows how to retain useful checks without acceptance-test narration.

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
- "Learning objectives" (required in every use case, localized as "学习目标" in Chinese)
- "In this guide, you will learn how to:"

### Lists: Steps vs Configuration Fields vs Sub-steps

**Numbered steps (1. 2. 3.)**: Use for sequential actions that must be performed in order.

**CRITICAL: Do not insert non-list text (e.g., "Then, configure it in Jaaz:") between numbered steps.** This breaks the Markdown numbered list and causes step numbering to reset. If you need to group steps logically, either use a comment or keep all steps in a single continuous list.

**Unordered lists (-)**: Use ONLY for:
- Multiple configuration fields/options (no specific order required, a table is also suitable)
- Prerequisites or requirements
- Feature lists
- Learning objectives and related-resource lists

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
- If it's **filling in configuration values**, use an unordered list or field table
- If it's **performing actions in sequence**, use `a. b. c.` (ordered sub-steps)

