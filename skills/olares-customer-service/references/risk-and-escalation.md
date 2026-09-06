# Risk and escalation

Use this reference whenever a ticket involves a potentially destructive action, sensitive information, or a policy/support boundary.

## Escalate rather than improvise

Require human or responsible-team review for:

- Data loss, backup integrity, restore failure, migration, deletion, factory reset, format, or reinstall
- Firmware, BIOS, boot failure, no display, no power, abnormal heat, fan, electrical, or other hardware-safety symptoms
- Security vulnerabilities, suspected compromise, leaked credentials, recovery codes, tokens, or private keys
- Olares ID recovery, identity verification, 2FA/TOTP reset, or account ownership disputes
- Licensing, third-party distribution rights, legal claims, refunds, warranty, and official support boundaries
- Unconfirmed roadmap, release date, fix version, or compensation

The draft may acknowledge the issue and collect safe minimum context, but it must not make a policy decision or provide an unverified destructive workaround.

## Destructive operations

Before recommending deletion, uninstall with data removal, reset, reinstall, format, firmware/BIOS changes, or migration:

1. Confirm that an authoritative source covers the customer's exact device and version.
2. State what data or configuration can be affected.
3. Require a verified backup when possible and explain how to verify it.
4. State the rollback or recovery path and the point after which it may no longer be available.
5. Prefer reversible diagnostic steps first.
6. Stop and escalate if the source, backup state, or device identity is uncertain.

## Diagnostic data and privacy

Ask only for data that can change the next decision. Prefer:

- Olares OS, app, and chart versions
- Approximate timestamp with timezone
- Exact error text or a narrowly cropped screenshot
- The relevant component's scoped log window
- Reproduction steps and the expected versus actual result

Do not request or expose passwords, API keys, session cookies, private keys, recovery codes, TOTP seeds, access tokens, full environment dumps, or unrelated log history. Treat Olares IDs, device identifiers, account details, email addresses, IP addresses, domains, and logs as potentially sensitive. Tell the customer what to redact and do not direct them to post sensitive material in public Discord, GitHub, or other public channels.

Do not invent a private upload destination. If no approved secure channel is available, escalate internally and tell the customer that secure submission instructions will follow.

## Commitments and ticket state

- A fix claim needs a source, a version, and a verification step.
- An ETA needs a tracked item and an accountable owner. Otherwise say no confirmed date is available.
- A handoff should name the responsible function when known and specify the event that will trigger the next update; do not invent a person or deadline.
- Do not recommend closing a ticket until an external conclusion exists and the resolution or next ownership is recorded.
- Suggested statuses are recommendations only; changing state requires explicit authorization.
