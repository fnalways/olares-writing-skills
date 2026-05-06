---
name: olares-ux-writing
description: Review and write bilingual (English/Chinese) UX copy for Olares products. Covers UI labels, error messages, notifications, empty states, confirmation dialogs, and onboarding. Enforces Olares-specific style, terminology, punctuation, accessibility, and localization rules. Use when editing or creating interface strings, reviewing i18n keys, or auditing product copy for consistency. For long-form documentation, see olares-docs-writer. For Chinese-to-English use case tutorials, see use-case-writer.
metadata:
  version: 0.1.0
---

# Olares UX Writing

Write and review user-centered interface copy for Olares products. This skill enforces the Olares UX writing and localization guidelines.

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

## Project-Specific Context

**Olares device**: Any hardware that has Olares OS installed, activated or not.

**Activation & ownership**: Only the device owner can activate via mDNS (requires physical access). After activation, the user becomes both owner and admin.

**Local password**: The device-local password (not "LarePass password"). It works only on the current device and protects Vault as well as other local security features.

**Wizard page / Wizard URL**: The activation page displayed after command-line installation of Olares. Users scan a QR code on this page to activate.

**Network discovery**: mDNS and LAN are implementation details. In user-facing copy, use `network` or `nearby` instead of `LAN` or `mDNS`.

**Security settings**: Use `Security`, not `Safety`, for the settings category that includes local password, biometrics, and Vault lock.

**Legacy brand name**: `Terminus` is an old brand name. Replace with `Olares` in all user-facing UI.

**Reused component labels**: Some button labels (e.g., `Confirm`, `Next`) are shared across multiple screens. Changing them affects consistency everywhere. Always check with the user before modifying widely reused strings.

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

Omit `a`, `an`, `the` in short labels (buttons, tabs, toasts, empty states) when the verb is unambiguous.
- ✅ `Create account`, `Add user`, `Open file`
- Keep articles in flowing prose and when dropping them causes ambiguity.

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
  - ✅ `Click **Save** to continue.`
  - ❌ `Click 'Save' to continue.`
- **Hyphenated compounds**: capitalize only the first word in sentence case.
  - ✅ `Read-only`, `Multi-node read-only`
  - ❌ `Read-Only`
- **Avoid repeated prepositions**: `Turn on Bluetooth on your phone` → `Your phone's Bluetooth must be on` or `Turn on your phone's Bluetooth`.

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

## UI Labels & Buttons

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

> Note: dialog titles use "New xxx" regardless of whether the trigger button says Create or Add.

### Referring to UI Elements in Text

- **Buttons and input boxes**: omit descriptor.
  - ✅ `Click **Continue**.` / `Enter your email address.`
  - ❌ `Click the **Continue** button.` / `Fill in the "Email" field.`
- **Tabs and checkboxes**: include descriptor.
  - ✅ `On the **Alignment** tab, clear the **User** checkbox.`
- **Unlabeled icons**: `the + function + icon`
  - ✅ `Click the color picking icon.`

## Confirmation Dialogs

Use only for irreversible or high-impact actions.

- **Title states the consequence directly.** No "Are you sure?"
  - ✅ `Delete this folder?`
  - ❌ `Are you sure?`
- **Omit description if the title is already clear.**
- **Use specific verbs for destructive actions.** `Delete`, `Remove`, `Discard` — not `OK` or `Yes`.
- **Unsaved changes**: use three buttons.
  - `Save` / `Don't Save` / `Cancel`

## UI Messages

### Embedded Messages (Helper Text, Tooltips, Empty States)

- **Helper text / tooltips**: imperative verb, single sentence → no end punctuation.
  - ✅ `Rebuild all indexes when toggled.`
  - ❌ `Rebuilds all indexes when toggled.`
- **Placeholder text**: don't repeat the label. Provide a format hint or prompt.
  - ✅ `Enter folder name`
  - ❌ `Folder name`
- **Clarity over brevity**: When the user emphasizes that the layout is adaptive or that explaining the scenario matters more than fitting on one line, do not force overly concise copy that sacrifices accuracy. Avoid marketing words like `Streamline` in instructional UI.

**Empty States**

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
- **Failure**: `Unable to + Verb + Object`
  - ✅ `Unable to add feed`, `Unable to rename file`
  - For verb-only: `Verb / Verb-ing + failed` (`Refresh failed`, `Binding failed`)

### Blocking Messages (Dialogs, Alert Bars)

- **Title**: start with an imperative verb that names the current task.
  - ❌ `Info`
  - ✅ `Set local password`
- **Description**: supplement the impact, don't restate the title.
  - ❌ Description: `This will delete the market source.` (restates title)
  - ✅ Description: `The operation cannot be undone.`
- **Delete description if there's no extra information.**
- **Every dialog must have a cancel/exit path.**

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

- [ ] Sentence case, no unnecessary end punctuation
- [ ] Second person ("you"), active voice (passive OK for explanatory/system text)
- [ ] Specific verb in button labels (1–3 words); check if label is reused across screens before changing
- [ ] Error message uses correct weight (`cannot` / `Unable to` / `Failed to` / `Invalid` / `Incorrect`)
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
