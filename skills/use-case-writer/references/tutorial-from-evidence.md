# Tutorials from evidence

Use this workflow for both conventional drafts and engineering inputs. Source notes are evidence, not the page outline.

## Define the task and select content

Identify the reader's starting state, one useful outcome, and the simplest supported path. Infer routine editorial choices from the material. Ask only when a missing fact materially changes the instructions.

| Material | Destination |
| --- | --- |
| Required action, value, or dependency | Main workflow or prerequisites |
| Observable state needed to continue | Beside the relevant action |
| Known limitation affecting the task | Relevant step, concise callout, or FAQ |
| Optional configuration with a user purpose | After the main path, a details block, or a precise link |
| Test IDs, coverage, hashes, retries, one-run measurements, build results | PR validation notes or an existing internal record |
| Unsupported claim or unknown required value | Explicit unresolved item in the draft and review summary |

Do not organize the tutorial around porting chronology, debugging sessions, pass/fail tables, or assertions. Do not create a separate public acceptance page merely to relocate these records. A requested diagnostic or verification guide has its own audience and scope.

Keep a limitation when it changes what the reader can do. Explain its symptom, scope, and supported next action. Removing test narration must not imply that an untested path is verified or that an unresolved issue is fixed. Do not delete evidence records just because they do not belong in the tutorial.

## Choose a useful example

Use a small, realistic task with value beyond testing a feature. Keep the same scenario across related steps and explain how to substitute the reader's own material.

- A scheduled world save teaches routine server administration better than a temporary player-count test.
- Related project documents can show why knowledge-graph relationships are useful.
- A saved preference recalled in a later conversation explains persistent memory.
- A research question followed by source review and export provides a complete result.

These are editorial examples. Confirm product support before using them. Label fictional data and do not claim generated examples were executed.

Pick an explicit example configuration for the first run. Distinguish it from defaults, hard requirements, and all supported options. Put the full option list where readers need it rather than listing every combination before starting.

## Keep Learning objectives

Every use case includes Learning objectives, or 学习目标 in Chinese, after the introduction. List the useful outcomes the guide actually teaches. Keep the list short, use action verbs, and avoid repeating the introduction or listing test coverage. Do not remove the section when shortening a guide or following an older merged example that omitted it.

## Make the steps usable

Explain where required values come from, which app or instance they belong to, and where to run commands. Avoid incomplete directions such as “obtain a reachable address” without a source. For tasks in scope, give usable steps or an accurate link. Mentioning SFTP alone does not teach file transfer.

Lead with working defaults when supported. Put alternate models, agents, distributions, and file-editing fallbacks after the main path. Explain unfamiliar components when needed to make a choice. Prefer UI instructions for UI tasks while keeping CLI actions where required.

Retain consequences that affect decisions or data: a clone might create a fresh installation, a disk might support expansion but not shrinking, and deleting app data might delete the system disk. Verify these per app and explain them beside the action.

## Keep checks that help the reader proceed

A check belongs when it tells the reader whether to continue, wait, or recover. Give the verified observable signal, its location, and the next action. Do not invent a status label.

Keep service readiness, a relevant startup marker, checking the intended memory bank, and a completed backup before replacing data. Installation can finish before a guest OS or model service is ready. Do not remove that distinction to make the prose lighter.

Avoid separate acceptance lists that repeat login, restart, export, or permission checks solely to reproduce test coverage. Include commands for the reader's current question, not because they appeared together in a diagnostic script.

For AI outputs, describe where to inspect the result and how to compare it with source material. Do not require fixed wording or promise identical generated entities. Preserve exact expected values when they are deterministic configuration or status values rather than variable AI output.

## Search for reuse before drafting

1. Search `docs/reusables/` and `docs/zh/reusables/` for the topic. Read candidate regions rather than trusting their filenames.
2. Check app/version, protocol, caller location, model route, and authentication assumptions against the task.
3. Read canonical guides and nearby use cases for required details and exceptions.
4. Search screenshots and check the UI state, model, and version before reusing one.

Useful searches:

```bash
rg --files docs/reusables docs/zh/reusables
rg -n 'Router|default-chat|embedding|endpoint|VPN' docs/reusables docs/zh/reusables
rg -n '@include:|How to call this model|Manage environment variables' docs/use-cases
```

Use a named-region include when the procedure belongs inline and fits. Link to a specific section for a separate prerequisite or optional background. Write app-specific differences locally. Reuse screenshots without copying them to new paths.

Check that include files and regions exist and render correctly at the including page, including nested lists and relative links. Chinese pages use matching localized fragments. Never replace a Chinese page with a whole English-page include.

For example, `ai-service-connections.md#use-different-model` was reused in several reviewed guides. Read its current content before using it. Do not make a historical model name or a particular fragment mandatory for every app.

Do not modify shared behavior merely to fit one app. Extract a new fragment only when multiple real consumers share its procedure and assumptions. When changing one, inspect its existing consumers in both languages. Briefly record meaningful reuse decisions in the PR, not as a new tutorial section.

## Review after the final change

Review the affected English and Chinese pages, metadata, gallery copy, and included content after all edits. Repeat after technical follow-ups or FAQ additions.

- Is the task coherent, with required Learning objectives and an example worth using?
- Are required inputs traceable and steps complete in the actual UI order?
- Are example values distinguished from defaults and requirements?
- Do checks help the reader continue or recover, without repeating acceptance tests?
- Are known limits and data-loss consequences still visible at the relevant action?
- Are shared text, canonical links, and matching screenshots reused appropriately?
- Do identifiers, endpoints, credentials, protocols, and instance paths match the actual connection?
- Does authored prose, including new technical notes, follow the punctuation and terminology rules?
- Do required pages, navigation, gallery entries, and localized links exist? Are includes and images valid?
- Does the PR accurately distinguish documentation checks from runtime checks and unresolved coverage?

Inspect semicolon and dash matches in context. Preserve code syntax, URLs, exact UI labels, compound-name hyphens, and numeric ranges. Keyword searches help locate problems but cannot judge tutorial quality. Report actual checks and unresolved facts without treating a formatting pass as proof of technical correctness.
