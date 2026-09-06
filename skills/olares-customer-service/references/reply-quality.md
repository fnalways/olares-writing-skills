# Reply quality and tone

Use this reference when drafting, reviewing, correcting, or translating an Olares customer-facing reply.

## What the ticket review showed

The August 2026 review examined 213 closed or resolved external conversations. It found that historical records are directional evidence rather than a clean gold set: many conversations lacked a recognizable external reply, and manually imported records sometimes mixed customer, community, and support voices.

Recurring reply failures were:

- Answering an adjacent question instead of the customer's actual question
- Giving an overconfident answer, then silently contradicting it later
- Presenting a guess such as a restart or refresh as a solution
- Promising “soon,” “next version,” or a date without a tracked owner and source
- Asking for full logs or identifiers without minimum scope, redaction, or a private channel
- Using greetings, apologies, praise, emoji, or “let us know” in place of a technical next step
- Closing a case without an auditable external conclusion
- Treating internal notes as acceptable training examples even when their wording was dismissive or unverifiable

Do not copy language from such records. Use them to identify failure modes and missing documentation.

## Customer-ready structure

Adapt the length to the case, but preserve this logic:

1. Confirm the specific symptom and environment in one sentence.
2. State the current conclusion and confidence boundary.
3. Give the shortest safe, source-backed action with the applicable version or UI path.
4. State the expected result and how to verify it.
5. Give the failure branch and request only the minimum diagnostic fields.
6. State how follow-up will be triggered. Give a date only when it is genuinely owned and traceable.

## Tone

- Match the customer's language and level of technical detail.
- Be calm, concise, respectful, and specific.
- Acknowledge disruption briefly when warranted; follow immediately with the concrete action.
- Do not blame the customer or imply that an undocumented limitation should have been obvious.
- Avoid filler greetings, repeated thanks, excessive apologies, praise, emoji, and exclamation marks.
- Explain unavoidable jargon the first time it appears.
- Separate confirmed facts from hypotheses.

## Corrections

When an earlier support answer was wrong or incomplete, say so explicitly:

- Identify the inaccurate statement.
- Give the corrected answer and its applicable version/scope.
- Explain whether earlier steps caused any risk or need to be reversed.
- Provide the verification step and source.

Do not quietly replace the answer or pretend the contradiction did not happen.

## Useful patterns

### Verified fix

“This issue is fixed in **[version]**. Confirm your version at **[path]**, then **[action]**. When complete, **[observable result]** should appear. If it does not, reply with **[minimum fields]** through **[approved channel]**.”

### Needs diagnosis

“The symptom can have more than one cause, so it is not yet safe to recommend a reset or reinstall. First, **[safe discriminating check]**. If you see **[result A]**, follow **[path A]**; if you see **[result B]**, send **[minimum fields]**.”

### Unsupported or unconfirmed

“This may be technically possible, but it is not currently documented as an officially supported configuration for **[scope/version]**. The supported alternative is **[option]**, with **[limitation]**. We do not have a confirmed release date for broader support.”

### Customer solved the issue

“Thanks for confirming the issue is resolved. Before closing the case, please confirm that **[specific action]** was the effective change and that you are using **[version/environment]**. We can then link the verified resolution to **[documentation location]**.”

Use these as logic patterns, not rigid scripts. Remove placeholders and unsupported promises before presenting a reply.
