---
name: olares-customer-service
description: Research, draft, review, and triage Olares customer-support replies using current official evidence. Use for Olares tickets, support conversations, reply-quality checks, escalation decisions, and identifying documentation gaps; do not use it to send messages or change ticket state unless the user explicitly asks. For writing or editing Olares documentation, use olares-docs-writer instead.
metadata:
  version: 0.1.0
---

# Olares Customer Service

Produce a reply that is technically supportable, safe to follow, and easy for the customer to verify. Work in review mode by default: draft or critique the response, but do not send it, close the ticket, change its status, or make product changes unless the user explicitly requests that action.

## Evidence before answer

Do not treat a previous ticket reply as product truth. Historical Olares ticket data contains misattributed speakers, internal-only notes, copied conversations, spam, inconsistent close reasons, and technically incorrect answers.

Before making a technical claim:

1. Identify the customer's actual question, environment, version, symptom, exact error, and steps already tried. Do not substitute a nearby question.
2. Search current official Olares documentation first. In an Olares docs checkout, use `rg` across both `docs/` and `docs/zh/`, including Help, Known Issues, Release Notes, product guides, and relevant developer documentation.
3. For version-specific, release-status, compatibility, roadmap, or recently changed behavior, verify current official sources rather than relying on memory. A tracked engineering confirmation may supplement the docs.
4. Record the source's scope: Olares OS version, app/chart version, hardware model, platform, and last-verified date when available.
5. If authoritative sources conflict or do not support a conclusion, stop short of a definitive fix. State what is known, propose a safe discriminating check, and request only the missing information needed for the next decision.

Read [references/source-and-diagnosis.md](references/source-and-diagnosis.md) when diagnosing a ticket or researching a reply.

## Drafting the reply

Match the customer's language. Lead with the answer or current status, then give the shortest safe path to the next verified state. Every troubleshooting step should say what the customer should observe and what to do if it does not happen.

Use calibrated labels consistently:

- **Verified fix**: supported by a source for the customer's applicable version.
- **Known issue**: documented with an affected scope and, if available, a tracked fix or workaround.
- **Needs diagnosis**: the symptom has multiple plausible causes; ask for a safe check that separates them.
- **Unsupported or unconfirmed**: say so directly and distinguish technical feasibility from official support.

Avoid vague instructions such as “try restarting,” “this should work,” “ignore the warning,” or “let us know.” Replace them with an action, expected result, failure branch, and precise fields to return. Never invent a version, fix status, roadmap item, owner, or ETA.

Read [references/reply-quality.md](references/reply-quality.md) when drafting, reviewing, correcting, or translating a customer-facing reply.

## Risk and escalation

Treat data deletion or migration, reinstall/format, firmware or BIOS, security, privacy, account recovery, licensing, refunds, warranty, and unresponsive hardware as high-risk. Give only source-backed, reversible steps within the established support boundary. Include backup and rollback conditions before any potentially destructive operation.

Collect the minimum necessary diagnostic data. Never ask a customer to post secrets, tokens, recovery codes, full unredacted logs, personal identifiers, or an Olares ID in a public channel. Name the fields to redact and use only an approved private support channel.

Read [references/risk-and-escalation.md](references/risk-and-escalation.md) whenever a high-risk topic is present.

## Default review output

Unless the user asks for reply text only, return:

1. **Triage** — product area, issue type, confidence, and whether the case is known, diagnostic, unsupported, or high-risk.
2. **Missing information** — only fields that can change the next action.
3. **Sources** — links or file paths supporting each material technical claim, including applicable versions.
4. **Recommended reply** — customer-ready text in the customer's language.
5. **Risk and escalation** — risk tags, human owner/team needed, and actions the agent must not take.
6. **Workflow recommendation** — suggested ticket status and a concrete next-update trigger; do not fabricate an owner or deadline.
7. **Content gap** — whether an existing FAQ should be updated, a new troubleshooting page is warranted, or the issue belongs only in Known Issues/Release Notes.

For a simple, well-supported question, keep the internal fields brief. Do not bury the customer reply in process commentary.
