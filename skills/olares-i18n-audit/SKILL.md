---
name: olares-i18n-audit
description: Audit Olares module i18n and UX copy across current-branch diffs before translation or release. Use when reviewing touched files, checking bilingual semantic alignment, scanning direct UI strings in code, preparing a module for Chinese or small-language localization, or verifying punctuation, placeholders, terminology, and title/body message quality. Pair with olares-ux-writing for the copy rules.
metadata:
  version: 0.1.0
---

# Olares i18n Audit

Use this skill to run a repeatable i18n and UX-copy audit for an Olares module. This skill defines the audit workflow; use `olares-ux-writing` for the writing rules and terminology decisions.

## Audit Scope

Audit the current branch against the target base unless the user gives a different range.

Include:
- i18n files for all touched locales
- UI code with direct user-visible strings
- native platform resources such as Android `strings.xml` and iOS plist/storyboard strings
- Electron locale JSON and desktop menu/update strings
- service/status strings that appear in UI

Do not limit the audit to files already named `i18n`. Branches often introduce user-visible strings in Vue, TypeScript, Kotlin/Java, Swift, JSON, and service layers.

## Standard Workflow

1. **Identify changed files**
   - Use `git diff --name-only <base>...HEAD` or the user-provided range.
   - Separate files into i18n, UI code, native resources, and non-copy files.
   - If the worktree is dirty, inspect current `git status --short` before editing and preserve unrelated user changes.

2. **Find changed user-visible strings**
   - Review i18n value changes, not only key changes.
   - Search code diffs for string literals in UI components, services, native resources, and JSON.
   - Treat console logs, class names, API paths, CSS, test data, and internal enum values as non-user-facing unless the code shows they are displayed.

3. **Check usage context**
   - Search for each key, object path, or literal value with `rg`.
   - Classify usage as title, body, placeholder, helper text, toast, dialog, empty state, notification, menu, or status.
   - For title/body pairs, review the rendered message as a pair. Do not make the body repeat the title.

4. **Audit semantic alignment**
   - For each locale pair, compare state, reason, next step, object, condition, severity, and placeholders.
   - Alignment does not require the same sentence count or word order.
   - If English is unclear or unfriendly, fix the English source before translating.

5. **Audit punctuation per locale**
   - Judge displayed values, not i18n keys.
   - Single-sentence UI values have no final period/full stop.
   - If one locale has one sentence and another has two, apply punctuation independently per locale.
   - Keep ellipses only for ongoing operations such as `Parsing content...`.
   - Keep question marks for real user decisions.

6. **Audit placeholders and markup**
   - Placeholders must match exactly across locales: `{name}`, `{version}`, `{domain}`, rich-text spans, and line-break tags.
   - Do not add hardcoded punctuation or quotes around placeholders unless the design explicitly requires it.
   - Verify localized text keeps required HTML tags and class-bearing spans when the source uses rich text.

7. **Audit terminology and formatting**
   - Keep Olares brand terms in English: `Olares`, `Olares OS`, `Olares ID`, `Olares Space`, `LarePass`, `Vault`, `Profile`, `Studio`, `Wise`.
   - Use exact spellings: `Wi-Fi`, `CPU`, `GPU`, `API`.
   - In Chinese, add spaces around Latin product/technical terms when readability needs it: `通过 Wise`, `系统 CPU`, `可用 GPU`.
   - Replace legacy `Terminus` with `Olares` in user-facing copy unless the product intentionally still uses the old name.

8. **Audit tone and readability**
   - Chinese: remove translationese, fragmented sentence chains, and unnecessary `你/你的/这个/该/此` when the subject is obvious.
   - English: avoid `Failed to`, `successfully`, unnecessary `Please`, `click/tap`, and overly formal phrasing.
   - Toasts should be concise outcomes: `Cookie uploaded`, `Update complete`, `Unable to upload cookie`.
   - Errors should tell users what happened and what to do next without blame.

9. **Decide and edit**
   - Edit directly when the issue is clear, context is known, and reuse risk is low.
   - Leave reusable generic labels alone unless they are clearly wrong in every context.
   - Mark unresolved items as `Needs UI context`, `Reuse risk`, or `Discuss` instead of guessing.

10. **Validate**
   - Run formatting for touched files when the repo provides a formatter.
   - Run `git diff --check`.
   - Re-run targeted searches for the exact issue class being fixed, such as single-sentence final periods or placeholder mismatches.

## Suggested Commands

Use these as starting points and adapt to the repo.

```bash
git status --short
git diff --name-only origin/main...HEAD
git diff --unified=0 origin/main -- <paths>
rg -n "key_or_literal" <paths>
git diff --check
```

To scan changed string literals, use targeted `git diff` plus `rg`. Review results manually; many hits are keys, CSS classes, API paths, or internal values.

```bash
git diff origin/main -- packages/app/src packages/app/config packages/app/src-capacitor \
  | rg '^\+[^+].*".{3,}"'

git diff origin/main -- packages/app/src packages/app/config packages/app/src-capacitor \
  | rg "^\+[^+].*'.{3,}'"
```

For punctuation audits, count sentences on displayed values only. Do not flag i18n keys just because the key contains punctuation.

## Output Format

When reporting, keep it actionable:

- **Changed**: summarize direct edits by module or issue type.
- **Checked**: list the files or file groups audited.
- **Left as is**: mention intentional exceptions, such as title/body pairs where the body omits repeated state information.
- **Needs follow-up**: only include items that require UI context, product decisions, or broader refactors.
- **Validation**: state which checks passed or could not be run.

## Stop Conditions

Stop and ask only when:
- the base branch or module scope is ambiguous and cannot be inferred
- a string is reused in incompatible contexts and changing it would create a product decision
- placeholders or markup differ but the rendering behavior is unclear
- the requested edits require changing behavior, not just copy
