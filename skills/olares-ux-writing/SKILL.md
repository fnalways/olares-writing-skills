---
name: olares-ux-writing
description: Review and write bilingual (English/Chinese) UX copy for Olares products. Covers UI labels, error messages, notifications, empty states, confirmation dialogs, and onboarding. Enforces Olares-specific style, terminology, punctuation, accessibility, and localization rules. Use when editing or creating interface strings, reviewing i18n keys, or auditing product copy for consistency. For long-form documentation, see olares-docs-writer. For Chinese-to-English use case tutorials, see use-case-writer.
metadata:
  version: 0.1.0
---

# Olares UX Writing

Write and review user-centered interface copy for Olares products. This skill enforces the Olares UX writing and localization guidelines.

Use Atlassian Design's content foundations as the closest external benchmark for UX/UI content design. Olares-specific terminology, product context, and localization rules take precedence when they differ.

## When to Use

- Writing or editing UI strings (buttons, labels, titles, messages, forms)
- Reviewing English source copy before translation
- Auditing product copy for consistency, clarity, and accessibility
- Creating error messages, notifications, empty states, or confirmation dialogs
- Designing onboarding or helper text

## Olares Brand & Terminology

**Brand terms (stay in English in all languages)**
`Olares`, `Olares OS`, `Olares ID`, `Olares Space`, `LarePass`, `Vault`, `Profile`, `Studio`, `Wise`

**Built-in app names (translate per target language)**
`Desktop`, `Market`, `Files`, `Settings`, `Control Hub`, `Dashboard`

**Exact spelling and capitalization**
- `CPU`, `API`, `Wi-Fi`, `Olares`, `LarePass`
- Never `Cpu`, `api`, `olares`, `larepass`, `WiFi`

For the full approved wordlist and glossary, see `wordlist.md` and `glossary.md` in the i18n directory.

**External content design reference**
- Atlassian Design Content: `https://atlassian.design/foundations/content/`
- Relevant sections: Style, grammar, and punctuation; Voice and tone; Designing messages; Inclusive language.

## Project-Specific Context

**Olares device**: Any hardware that has Olares OS installed, activated or not.

**Activation & ownership**: Only the device owner can activate via mDNS (requires physical access). After activation, the user becomes both owner and admin.

**Local password**: The device-local password (not "LarePass password"). It works only on the current device and protects Vault as well as other local security features.

**Wizard page / Wizard URL**: The activation page displayed after command-line installation of Olares. Users scan a QR code on this page to activate.

**Network discovery**: mDNS and LAN are implementation details. In user-facing copy, use `network` or `nearby` instead of `LAN` or `mDNS`.

**Security settings**: Use `Security`, not `Safety`, for the settings category that includes local password, biometrics, and Vault lock.

**Legacy brand name**: `Terminus` is an old brand name. Replace with `Olares` in all user-facing UI.

**Reused component labels**: Some labels (for example `Name`, `Password`, `File`, `Confirm`, `Next`) are shared across multiple screens. Changing them affects consistency everywhere. Treat shared labels as reuse-sensitive and check usage before changing their value.

## i18n Review Workflow

Use this workflow when reviewing changed i18n files or editing localized UI copy. The workflow must stand on its own; do not depend on a browser plug-in or VS Code extension being available.

1. **Separate key from value.**
   - Default to editing values only.
   - Do not rename i18n keys unless the user explicitly asks for it or the code references are updated in the same change.

2. **Check usage before judging the copy.**
   - Search the repo for the key, object path, or literal value using available project tools.
   - If the user or repo provides reuse notes, use them; do not assume a specific support file exists.
   - When relevant, inspect how the UI renders the value: plain text, placeholder, helper text, rich text, toast, dialog, or title.

3. **Classify usage risk.**
   - **No references found**: mark as `Orphan candidate`. Do not delete it unless the user asks for cleanup.
   - **One reference found**: optimize against that UI context.
   - **Multiple references found**: mark as `Reuse risk`; keep the value generic unless it works for every context or a context-specific key is added.
   - **Dynamic or unresolved references**: mark as `Needs UI context`; do not assume it is unused.

4. **Decide whether to edit, discuss, or leave unchanged.**
   - Edit directly only when the issue is clear, context is known, and reuse risk is low.
   - Mark for discussion when the copy is UX-compliant but questionable for user habits, industry terms, product intent, or UI constraints.
   - Keep generic labels generic when they are reused: `Name`, `Password`, `File`, `Bucket`, `Confirm`, `Next`.

5. **Do not mark by adding comments blindly.**
   - Use the review output to mark issues.
   - Do not add TODOs, inline comments, or i18n comments only to flag a review concern.
   - Add a comment only when the user asks for persistent in-file documentation or when an existing repo convention requires it.

### Review Output Categories

When useful, group findings by decision type:

- **Must fix**: inaccurate, misleading, broken, inaccessible, or inconsistent with required terminology.
- **Reuse risk**: the value is used by multiple screens or appears to be a generic field label.
- **Orphan candidate**: no references found; do not delete without a cleanup decision.
- **Needs UI context**: rendering, component behavior, or runtime path is unclear.
- **Discuss**: acceptable by UX writing rules, but questionable for industry norms, user habits, or the actual scenario.
- **Leave as is**: deliberately unchanged because the current copy is safer or more reusable.

## Core Principles

1. **Friendly and conversational**, not formal or entertaining.
2. **Use "you."** Use "we" only in system-initiated messages (errors, status updates).
3. **Sentence case everywhere in UI.** Capitalize only the first word and proper nouns.
   - ✅ `Add source`
   - ❌ `Add Source`
4. **Simple present tense.** Use contractions outside of error messages.
   - ✅ `Files sync automatically.`
   - ❌ `Files will be synchronized automatically.`
5. **Active voice by default.** Use passive only to avoid blame, when the action matters more than the actor, or for explanatory text that describes system behavior.
   - ✅ `Your data is encrypted at rest.`
   - ✅ `Vault is protected by your local password.` (explanatory)
   - ❌ `We encrypt your data at rest.`
6. **Omit end punctuation on single-sentence UI text.** Titles, buttons, labels, placeholders, list items, single-sentence toasts, and single-sentence errors have no period. Use periods only when a message contains two or more sentences.
   - ✅ `Enter your email address`
   - ❌ `Enter your email address.`
7. **Front-load key information.** Lead with what matters most.
   - ✅ `Files larger than 2 GB cannot be uploaded.`
   - ❌ `Due to system limitations, files that exceed 2 GB in size are not able to be uploaded at this time.`
8. **Keep sentences under 25 words.** Split or restructure longer sentences.
9. **Match tone to the user’s state.**
   - Blocked, confused, or under pressure: be practical, direct, and reassuring. Give only what they need and the next action.
   - Successful or finished: be concise; add warmth only for meaningful, low-frequency moments.
   - New concept or onboarding: be more explanatory, but still short and scannable.
10. **Design the message, not just the sentence.** Identify whether the text is an error, warning, success, information message, empty state, or feature discovery before editing it.

### Please and Sorry

Use courtesy words only when:
- The system caused the problem, or
- The next step is a single short verb that sounds abrupt without "please."

- ✅ `Indexing might take a few minutes. Please wait.`
- ✅ `DNS resolution failed. Please try again.`
- ❌ `Please enter your email address.`

## Word Choice

### Prefer Simpler Words

| ✅ Use | ❌ Avoid |
|--------|----------|
| use | utilize, make use of |
| to | in order to |
| also | in addition |
| tell | inform, let know |
| remove | extract, eliminate, destroy |
| start | commence, initiate |
| end | terminate, finalize |
| help | facilitate, assist |
| show | display, indicate, demonstrate |
| get | obtain, acquire, retrieve |
| need | require, necessitate |
| about | approximately, roughly |
| enough | sufficient |
| because | due to the fact that |
| if | in the event that |
| before | prior to |
| after | subsequent to |
| try | attempt |
| let (you) | allow (you to), enable (you to) |
| set up | configure, establish |
| turn on | activate |
| turn off | deactivate |
| enter | input, type (for input fields) |
| because | due to the fact that |
| because of | due to |

### Abbreviations and Short Forms

- Avoid `e.g.`, `i.e.`, `etc.`, and `&` in customer-facing UI. They are less localizable and can be confusing for assistive technologies.
  - ✅ `For example`
  - ❌ `e.g.`
  - ✅ `and`
  - ❌ `&`
- Use the full name of features, apps, and concepts the first time they appear unless space is severely constrained.
- Do not use apostrophes for plural abbreviations.
  - ✅ `1990s`, `APIs`
  - ❌ `1990’s`, `API’s`

### Platform-Neutral Interaction Verbs

Avoid `click` and `tap`.

| Verb | Usage |
|------|-------|
| Select | Buttons, links, list items, menu items (general) |
| Select / Clear | Checkboxes (not check/uncheck) |
| Enter | Input fields (not input or type) |
| Choose | Preference-based selection, or when UI element name starts with "Select" |
| Turn on / Turn off | Toggles |
| Open / Close | Apps, panels, dialogs, files |
| Go to | Navigation to menus, tabs, pages |
| Switch | Between modes or views |
| Expand / Collapse | Content areas |
| Drag | Moving elements (not "drag and drop") |

### Fixed Spellings

Write these exactly:
- `Wi-Fi` (not `WiFi`)
- `read-only` (not `readonly`)
- `plug-in` (not `plugin`)
- `real-time` (adj.) / `in real time`
- `webpage` (not `web page`)
- `home page` (not `homepage`)
- `checkbox` (not `check box`)

### Articles in UI

Omit `a`, `an`, `the` in buttons, labels, tabs, and action-based headings when the verb is unambiguous.
- ✅ `Create account`, `Add user`, `Open file`
- Keep articles in flowing prose and when dropping them causes ambiguity.
- Keep articles in empty states and explanatory body copy when they make the text more natural or easier to translate.

## Error Message Vocabulary

Different error words carry different weight.

| Word | Usage |
|------|-------|
| **cannot** | Irreversible operations and legal/policy restrictions. Formal. |
| **can't** | Standard limitations outside of error contexts. |
| **Unable to** | Temporary obstacles (network, permissions). **Prefer this over "Failed to" in user-facing UI.** |
| **Failed to / Xxx failed** | Technical contexts where identifying the failed component matters. |
| **Error** | System-level problems (crashes, timeouts). Must explain cause or next action. |
| **Invalid** | Format/syntax violations. Include a valid format example if one exists. |
| **Incorrect** | Format is correct but the value is wrong. |

- ✅ `This operation cannot be undone.`
- ✅ `Unable to connect to the server.`
- ❌ `Failed to connect to the server.` (prefer "Unable to" for user UI)
- ❌ `Invalid password.` (use `Incorrect password.`)

**In error messages, always use `cannot`, never `can't`.**

## Punctuation & Formatting

### End Punctuation Rules

| Location | Punctuation |
|----------|-------------|
| Page titles, subtitles | None |
| Buttons, menus, navigation, placeholders, list items | None |
| Dialog body (single sentence) | None |
| Dialog body (multiple sentences) | Period on each sentence |
| Error messages (single sentence) | None |
| Error messages (multiple sentences) | Period on each sentence |

### Other Rules

- **Slash**: no spaces around it. `Richtext/Markdown`
- **Number + unit**: add a space. `71.82 MB`, `100 GB`
- **Multiplication sign**: use `×` with spaces. `400 × 400`
- **Number ranges**: use en dash `–` without spaces. `8–32 characters`
- **Time ranges**: use `to` with spaces. `10:00 AM to 2:00 PM`
- **Oxford comma**: use in lists of 3+. `Android, iOS, and Windows`
- **Exclamation mark**: only for genuinely positive moments. Use no more than one.
- **Ellipsis**: only for ongoing operations. Never in buttons or menus.
  - ✅ `Parsing content...`
  - ❌ `Parsing content. Please wait...`
- **No colon after field labels.** `Username` not `Username:`
- **Bold UI element names.** No quotes or italics.
  - ✅ `Select **Save** to continue.`
  - ❌ `Select 'Save' to continue.`
- **Quotation marks and apostrophes in UI copy**:
  - Use curly apostrophes in user-facing prose: `don’t`, `you’re`, `device’s`.
  - Use quotation marks sparingly. For direct quotations or cited text in UI prose, use curly double quotation marks: `“...”`.
  - Use single quotation marks only for nested quotations or when defining/emphasizing a word. Do not use single quotation marks around UI elements, product names, placeholders, or links.
  - Do not use quotation marks to emphasize UI controls, page titles, app names, or surface names. Use bold when the UI supports rich text; otherwise write the name plainly.
  - Code, commands, literal strings, file paths, and i18n object syntax may use straight quotes as required. Do not treat TypeScript string delimiters as user-facing punctuation.
  - ✅ `Select **Agree** to accept these terms.`
  - ✅ `Select Agree to accept these terms.` (when rich text is unavailable)
  - ❌ `Select “Agree” to accept these terms.`
  - ❌ `Open 'Files' to manage your documents.`
- **Hyphenated compounds**: capitalize only the first word in sentence case.
  - ✅ `Read-only`, `Multi-node read-only`
  - ❌ `Read-Only`
- **Avoid repeated prepositions**: `Turn on Bluetooth on your phone` → `Your phone’s Bluetooth must be on` or `Turn on your phone’s Bluetooth`.

## Numbers, Dates & Times

- **Body copy 0–9**: spell out. `five databases`
  - Exception: measurements (`3 GB`, `5 min`), space-constrained UI, and never start a sentence with a numeral.
- **4+ digits**: add commas. `1,024` / `65,536`
  - Exception: years and pixel dimensions.
- **Percentages**: body copy uses "percent." UI labels use `%`.
- **Dates**: spell out month, no ordinals. `June 1, 2025`
  - In a sentence: `The June 1, 2025, update includes...`
- **Time**: AM/PM uppercase with space. `10:45 AM`, `3 PM`
  - Use `noon` and `midnight` instead of `12:00 PM` and `12:00 AM`.
- **Time abbreviations**: `d`, `hr`, `min`, `sec`. `5 min`, `1 hr`, `30 sec`
- **Progress count**: use `of`, not `/`, when space allows.
  - ✅ `Step 1 of 2`
  - ❌ `Step 1/2`

## UI Labels & Buttons

### Titles and Headings

- Use sentence case and no end punctuation.
- Prefer action-oriented headings when the screen or dialog is task-based.
  - ✅ `Create work item`
  - ❌ `Creating a work item`
- Avoid gerunds for UI headings unless they describe a temporary system state.
- Avoid question titles unless the user must make a decision.
- Keep warning and error titles scannable. They should state what happened or what may happen, not explain the full next step.

### Button Labels

- Reflect the **specific action** in 1–3 words.
- Use imperative verb form.
- Avoid generic labels: `Confirm`, `OK`, `Done`.

| Button | Usage |
|--------|-------|
| New | Dialog title for creating objects (`New user`) |
| Create | Confirm button inside a creation dialog |
| Add | Add an existing object to a new environment |
| Delete | Permanent destruction |
| Remove | Take out of a list or group; object still exists |
| Save | Persist changes to existing content |
| Apply | Changes take effect immediately |
| Got it | User only needs to acknowledge |
| Next / Back | Multi-step wizard (not Previous) |
| Finish | Complete a series of steps (not Confirm) |
| Cancel | Cancel and return to previous state |

**Header + Button Pairings**

| Scenario | Header | Buttons |
|----------|--------|---------|
| New / Add | New [object] | Create, Cancel (or Add, Cancel) |
| Edit properties | Edit xxx | Save, Cancel |
| Modify (password, avatar, permissions) | Change xxx | Save, Cancel |
| Delete | Delete xxx | Delete, Cancel |

> Note: dialog titles use `New xxx` regardless of whether the trigger button says Create or Add.

### Referring to UI Elements in Text

- **Buttons and input boxes**: omit descriptor.
  - ✅ `Select **Continue**.` / `Enter your email address.`
  - ❌ `Select the **Continue** button.` / `Fill in the "Email" field.`
- **Tabs and checkboxes**: include descriptor.
  - ✅ `On the **Alignment** tab, clear the **User** checkbox.`
- **Unlabeled icons**: `the + function + icon`
  - ✅ `Select the color picker icon.`
- Avoid `>` in navigation paths because assistive technologies may read it as "greater than."
  - ✅ `Go to **Settings**, then **Network**.`
  - ❌ `Go to **Settings** > **Network**.`

## Confirmation Dialogs

Use only for irreversible or high-impact actions.

- **Title states the decision or consequence directly.** No "Are you sure?"
  - ✅ `Delete this folder?`
  - ❌ `Are you sure?`
- **Omit description if the title is already clear.**
- **Use specific verbs for destructive actions.** `Delete`, `Remove`, `Discard` — not `OK` or `Yes`.
- **Unsaved changes**: use three buttons.
  - `Save` / `Don't Save` / `Cancel`

## UI Messages

### Message Anatomy

- Start by identifying the message type:
  - **Error**: a problem has already occurred. Explain what happened and how to move forward.
  - **Warning**: a potential problem may happen if the user continues. Explain the consequence before the action.
  - **Success**: confirm the outcome, then get out of the way.
  - **Information**: add context that helps the user decide or understand.
  - **Empty state**: explain why there is no content and what the user can do next.
  - **Feature discovery**: explain why the feature matters and what to try next.
- Keep body copy to 1–2 sentences.
- Do not repeat the title in the body.
- If the reason is unknown, do not invent one. State that something went wrong and offer a next step.
- Avoid sending the user elsewhere for basic context. If support content is necessary, use a descriptive link.

### Title Pattern by Message Type

Use the title pattern that matches the message type:

| Message type | Title pattern | Example |
|--------------|---------------|---------|
| Task dialog | Imperative verb + object | `Set local password` |
| Confirmation | Decision or consequence | `Delete this folder?` |
| Error | What failed or what is blocked | `Unable to connect` |
| Warning | Possible consequence | `Your bill may increase` |
| Success | Outcome | `Profile updated` |
| Empty state | Current state | `No passwords yet` |

Do not force an imperative title onto errors, warnings, confirmations, or empty states.

### Embedded Messages (Helper Text, Tooltips, Empty States)

- **Helper text / tooltips**: imperative verb, single sentence → no end punctuation.
  - ✅ `Rebuild all indexes when toggled.`
  - ❌ `Rebuilds all indexes when toggled.`
- **Placeholder text**: don't repeat the label. Provide a format hint or prompt.
  - ✅ `Enter folder name`
  - ❌ `Folder name`
- **Clarity over brevity**: When the user emphasizes that the layout is adaptive or that explaining the scenario matters more than fitting on one line, do not force overly concise copy that sacrifices accuracy. Avoid marketing words like `Streamline` in instructional UI.

**Field Labels, Optionality, and Helper Text**

- Field labels name the data; helper text explains constraints, examples, consequences, or context.
- Do not duplicate optionality in both the label and helper text.
- Use label-level optionality (`Bucket (optional)`) only when there is no helper area and the optional status needs to be visible while scanning.
- Use helper text (`Optional`) when the component has a dedicated hint/helper area or the label is reused.
- Do not use placeholders as labels. Use placeholders only for examples or expected formats.

**Empty States**

- Use an informative, scannable title.
- Include the reason for the empty state and a next step when one exists.
- If the user finished or cleared a task, acknowledge completion instead of implying an error.
- Keep empty-state CTAs specific, imperative, and 1–2 words.
- Avoid too many CTAs on one page.

| Scenario | Use | Avoid |
|----------|-----|-------|
| No data yet (display only) | No data to display | No data available |
| Encourage user action | No projects yet. Create a project. | No data available |
| Real-time data empty | No recent activity | No data available |
| Static history empty | No history records | No data available |
| Search/filter no results | No results found | No matching results found |
| User cleared content | All cleared / You're up to date | No data available |
| System/permission issue | Access denied / Something went wrong. Wait a moment and try again. | Something went wrong |

### Transient Messages (Toasts)

- **Success**: `Object + Verb-ed`. Never use "successfully" or "success."
  - ✅ `Folder added`, `Profile updated`, `App installed`
  - For verb-only: past participle (`Copied`, `Refreshed`, `Saved`)
  - When unclear: `Verb-ing + completed` (`Binding completed`)
  - Do not add a CTA unless there is a useful follow-up.
  - Repeated success messages should be brief and low on delight.
- **Failure**: `Unable to + Verb + Object`
  - ✅ `Unable to add feed`, `Unable to rename file`
  - For verb-only: `Verb / Verb-ing + failed` (`Refresh failed`, `Binding failed`)
- **Warnings**: tell the user the potential consequence before the action. Avoid playful wording.
  - ✅ `Your bill may increase`
  - ❌ `Time to pay up!`

### Blocking Messages (Dialogs, Alert Bars)

- **Task dialog title**: start with an imperative verb that names the current task.
  - ❌ `Info`
  - ✅ `Set local password`
- **Description**: supplement the impact, don't restate the title.
  - ❌ Description: `This will delete the market source.` (restates title)
  - ✅ Description: `The operation cannot be undone.`
- **Delete description if there's no extra information.**
- **Every dialog must have a cancel/exit path.**
- For warnings and errors, CTA labels should be specific imperative verbs. Avoid `OK`, `Done`, `Yes`, and `No` unless they are truly the clearest choices.
- For errors, prefer `we` or neutral phrasing when naming the problem would otherwise blame the user.
  - ✅ `The connection was interrupted`
  - ❌ `You lost the connection`
- For high-risk destructive actions, state the consequence before the button.

### Lists in UI Copy

- Keep list items parallel.
- Fragment list items: lowercase, no end punctuation.
- Complete-sentence list items: capitalize each item and end each with a period.
- Use numbered lists only when order matters.
- Keep lists short. If there are more than six items, split them into groups.

### Notifications

- **Title**: under 50 characters, sentence case, no end punctuation.
  - ✅ `Backup completed`
  - ❌ `Your backup has been successfully completed`
- **Body**: 1–2 sentences, include next step if relevant.
- Don't repeat the app name. Send only when the user needs to know or act.

## Inclusive & Accessible Writing

- **Replace loaded terms**: `blocklist/allowlist`, `primary/secondary`, `stop/terminate`, `built-in`.
- **Gender-neutral**: singular `they/their/them`. Gender-neutral job titles (`chairperson`, `workforce`, `spokesperson`).
- **People-first language**: `users with low vision`, `living with`, `nondisabled person`.
- **Alt text**: describe function, not appearance. Under 150 characters. Capitalize first word, end with period.
- **Accessibility labels**: start with a verb, omit control type.
  - ✅ `Add` (announced as "Add, button")
  - ❌ `Add button` (announced as "Add button, button")
- **Descriptive links**: link text should make sense out of context.
  - ✅ `Learn more about [Olares backup].`
  - ❌ `Click here to learn more.`
- **Input-agnostic directions**: avoid "on the left" or "below" as the only locator. Don't use ALL CAPS in body text.

## Localization & Internationalization

Write source English so it translates cleanly.

- **One idea per sentence.** Keep it under 25 words.
- **Keep "optional" grammar words** (`that`, `who`, `which`, `the`, `a/an`) in flowing prose. They help translators parse structure.
  - ✅ `Verify that the account is active.`
  - ❌ `Verify the account is active.`
- **Don't stack more than two nouns as modifiers.**
  - ✅ `CPU usage limit for the cache`
  - ❌ `cache CPU usage limit`
- **Avoid idioms, sports metaphors, and culture-specific references.**
- **Never concatenate strings in code.** Use full strings with placeholders.
  - ✅ `You have {count} new messages`
  - ❌ `"You have " + count + " new messages"`
- **Use the same word for the same concept** across the product.
- **Allow 30–40% extra space** in fixed-width UI elements (German is the worst case).
- **Don't hardcode format or punctuation around placeholders.** Dates, times, and quotes should be handled by code or locale, not baked into source strings.
  - ❌ `Running time: 60 d 6 hr 20 min 20 sec` (hardcoded units)
  - ✅ `Running time: {duration}`
  - ❌ `Connected to Wi-Fi '{networkName}'` (hardcoded quotes)
  - ✅ `Connected to Wi-Fi {networkName}`
  - If a variable value needs visual separation, use UI layout, rich text, or locale-aware formatting instead of hardcoded quotes.
- **Singular vs plural**: Titles often use plural for scan results (`No Olares devices found`), while body copy may use singular for the user's specific device (`Make sure your Olares device is on the same network`). This is natural in English and does not need forced uniformity.

### Placeholders & Plurals

- Preserve placeholders exactly: spelling, casing, braces, order.
- **Don't use `(s)` for plurals.** Use abbreviations (`{minutes} min`), move the variable to the end (`Files uploaded: {count}`), or use your i18n framework's plural rules.

### Text Expansion Reference

| English Length | Reserve Space |
|----------------|---------------|
| 1–10 chars | 200–300% |
| 11–20 chars | 150–200% |
| 21–30 chars | 130–180% |
| 31–50 chars | 140–160% |
| 51–70 chars | 130–150% |
| 70+ chars | 130% |

## Review Checklist

Before finalizing any UI string:

- [ ] Key and value are separated; do not rename keys unless code references are updated
- [ ] Usage checked: no references, one reference, multiple references, or dynamic/unresolved
- [ ] Reuse risk handled before editing generic labels such as `Name`, `Password`, `File`, `Bucket`, `Confirm`, and `Next`
- [ ] Review concerns are marked in the report, not by adding comments to i18n files unless explicitly needed
- [ ] Sentence case, no unnecessary end punctuation
- [ ] Curly apostrophes in user-facing prose; no quotation marks around UI controls or app names
- [ ] Second person ("you"), active voice (passive OK for explanatory/system text)
- [ ] Message type identified first: error, warning, success, information, empty state, or feature discovery
- [ ] Tone matches user state: practical for blocked/error states; warmer only for successful or low-frequency moments
- [ ] Specific verb in button labels (1–3 words); check if label is reused across screens before changing
- [ ] Error/warning/success/empty-state body is 1–2 sentences and does not repeat the title
- [ ] Error message uses correct weight (`cannot` / `Unable to` / `Failed to` / `Invalid` / `Incorrect`)
- [ ] CTAs use specific imperative verbs; avoid `OK`, `Done`, `Yes`, and `No`
- [ ] Avoid `e.g.`, `i.e.`, `etc.`, and `&` in customer-facing UI
- [ ] No idioms, sports metaphors, or culture-specific references
- [ ] No string concatenation; placeholders use the codebase standard
- [ ] No hardcoded dates, times, units, or punctuation around placeholders
- [ ] No more than two stacked noun modifiers
- [ ] Plural-sensitive strings avoid `(s)`
- [ ] Olares brand terms spelled and capitalized correctly; no legacy `Terminus`
- [ ] Inclusive language (no `blacklist/whitelist`, no `master/slave`, gender-neutral)
- [ ] Accessible (descriptive links, no ALL CAPS, no direction-only instructions)
- [ ] Preposition accuracy (e.g., `LarePass as your provider`, not `autofill for LarePass`)
- [ ] iOS steps use general paths if the user needs cross-version compatibility
