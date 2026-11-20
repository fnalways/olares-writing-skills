---
name: olares-market-weekly
description: When the user wants to prepare Olares Market weekly app roundups, use this skill for English poster copy, Discord announcements, X and Facebook posts, Feishu draft updates, and editable SVG or Figma posters. Triggers on phrases like "weekly app updates", "Market roundup", "this week's app news", and "weekly Market poster". For full app tutorials, see use-case-writer. Not for app installation or packaging.
metadata:
  version: 0.1.0
---

# Olares Market Weekly

Produce a concise, accurate weekly roundup in the established Olares style. Treat approved poster copy as the content source for the visual. Cover only the deliverables the user requests.

## Choose the current stage

- **Research or draft:** Read the current release source and prior approved example. Show proposed English copy in chat when the user wants to review it first.
- **Discuss or revise wording:** Offer the requested alternatives without writing to Feishu or modifying the poster. Do not treat a preference discussion as permission to save every suggestion.
- **Save approved copy:** When the user says to update the document, or clearly accepts a concrete proposed update, make that change without asking for redundant confirmation.
- **Produce the poster:** Use the latest approved poster copy and existing visual style. Deliver an editable SVG or update the specified Figma file, according to the request.
- **Publish:** Preparing or saving drafts does not authorize posting to Discord, X, or Facebook.

A direct instruction to update this week's draft in Feishu authorizes the requested writing. Do not impose an extra approval gate. If the user says “show me first” or “do not update,” keep changes in chat until they approve saving them.

## Gather the right material

1. Read the supplied current-week release document. Identify its reporting dates and production status. Do not equate today's date with the source interval.
2. Read the most recent approved section of the destination document for structure, tone, and formatting. A link to an older Discord heading may simply identify the recurring document, not instruct you to overwrite that week.
3. Identify newly listed apps, updates to existing apps, removals, tutorials, and explicit exclusions. Merge repeated updates to the same app and use the version actually in production.
4. Check live official tutorials for advertised workflows, prerequisites, and availability. Read upstream release notes or packaging manifests when a material detail remains unclear.
5. If a source conflicts with a tutorial or deployed behavior, omit the disputed claim from promotional copy and flag the discrepancy briefly. Resolve it before presenting it as a feature.

Keep a compact local fact record when the task spans copy and graphics. Record the app name, production version, user benefit, meaningful requirement or change, and supporting source. Do not paste the research log into the announcement.

## Decide what deserves space

Choose benefits a user can recognize: a new way to work, useful editing controls, improved recovery, faster everyday operations, or a meaningful platform expansion.

Separate three kinds of information:

- **Highlights:** What people can now do, or what works better.
- **Actionable notices:** What a user must do before updating or on first use.
- **Specialist details:** Commands, plugin migrations, configuration, or narrowly affected setups. Keep these in a compact note or targeted follow-up when relevant.

Include notices that change a user's decision or prevent a failed workflow. Typical examples are a required data backup, irreversible migration, separate first-login credentials, changed attachment handling, GPU-specific availability, or unusually large hardware requirements. Explain the reason briefly. Do not add a general warning checklist to every roundup.

When assessing whether copy is too thin, look for omitted user benefits and consequential behavior changes. Do not add patch-list detail just to increase length.

## Fact boundaries

- Distinguish upstream app changes from Olares packaging or integration fixes. Do not attribute a platform limitation or vulnerability to either party without evidence.
- Check for functional changes as well as security fixes. Do not label a whole update “security updates” when that omits the useful story. State material security facts accurately without implying that Olares as a whole is unsafe.
- A delisting does not establish its cause, a replacement relationship, automatic migration, or loss of access for existing installations. Establish those separately through evidence or explicit user confirmation.
- If a model, integration, plugin, GPU edition, or additional service is required, preserve that qualification in the relevant claim.
- Keep product version, chart version, model variant, and minimum Olares version distinct.
- Do not infer a new app is live from a placeholder. When launch is confirmed, replace placeholders consistently across requested deliverables.
- Reassess dependent entries when an app is excluded. A plugin whose only purpose is the excluded app should normally be deferred too, with a brief explanation.
- Historical examples are style references, not facts about this week. Recheck requirements, commands, links, and versions.

## Writing preferences

Write publishable copy in English unless requested otherwise. Discussion with the user may remain in Chinese.

- Use plain, conversational language and concrete benefits. Avoid a technical release-note voice in social introductions.
- Do not use semicolons in public copy.
- Do not use middle dots or similar round-dot separators. Use natural sentences, line breaks, spacing, or hyphen-led lists. App names and versions can occupy separate visual elements.
- Avoid app counts in titles, introductions, and badges unless specifically requested.
- Do not use the phrase “upgrade notes.” Give the actual action and reason instead.
- Do not elevate one app into the week's main story without a reason or user preference.
- Do not force a slogan, a question, or a community-sharing request into every ending.
- Avoid presenting invented personal experience as fact. First-person enthusiasm is appropriate only when supplied or endorsed by the user.
- When asked for alternatives, provide several meaningfully different options. Do not repeat nearly identical paraphrases.
- When asked only about a main post or one sentence, keep the response to that scope.

For channel structure and examples, read [Channel copy](references/channel-copy.md). For SVG or Figma work, read [Poster production](references/poster-production.md).

## Feishu editing

Use the available `lark-doc` skill and its current instructions for reads and writes. If it is not installed, use an available supported Feishu connector or authorized UI workflow. Read fresh content and block IDs before editing when using block-based tools.

- Add the new reporting week as its own section in the existing chronological structure, normally newest first. Preserve the template, prior weeks, media, citations, and unrelated user edits.
- Reuse the existing section labels, typically `Poster copy`, `Discord`, and `X`. Add `Facebook` only when a separate Facebook draft is requested. Optional internal editorial notes belong outside publishable copy.
- Update the exact approved paragraph or block. Do not rewrite the whole document to revise a closing sentence.
- After replacing or deleting blocks, refresh affected IDs before further edits.
- Verify saved content by reading it back. Keep local source files aligned with approved copy so rebuilding an SVG cannot restore old text.
- When a change is shared across the poster and social copy, synchronize the affected requested outputs. Do not silently rewrite unrelated posts or old weeks.

## Locate project resources

Use the release source, draft archive, Figma file, and working directory supplied by the user or available in the current project context. Do not embed personal filesystem paths, internal document URLs, or remembered node IDs in the shared workflow.

Read the latest approved weekly section and poster before adapting them. Previous `Olares-Market-YYYY-MM-DD` folders can be useful style references, but their content is historical.

Do not assume a supplied Figma node still resolves to the desired page or frame. Inspect the file and preserve earlier posters.

## Completion

Return the actual result: a link to the updated Feishu section, the verified Figma frame, or a downloadable SVG, as requested. State briefly what changed and any unresolved limitation. If a connector fails or the computer is locked, complete independent local preparation, explain the blocker, and do not claim the external update succeeded.
