# Source and diagnosis workflow

Use this reference when researching or diagnosing an Olares ticket.

## Source hierarchy

Prefer evidence in this order:

1. Current official Olares documentation that matches the customer's product, version, hardware, and access path.
2. Official Known Issues and Release Notes with explicit affected and fixed versions.
3. A traceable engineering issue or product-team confirmation that states scope and current status.
4. A previously resolved external ticket only when its speaker, environment, resolution, and supporting source are verified.

Community messages, blogs, videos, internal notes, and old ticket replies can provide search terms or hypotheses. Do not use them as the sole authority for a fix, compatibility claim, support boundary, or ETA.

## Retrieval sequence

Extract before searching:

- Customer goal and exact question
- Olares OS version
- App and chart version, if applicable
- Olares One or other hardware model
- Client OS, browser, network path, and whether access is local, VPN, or public
- Exact status, error text, time observed, and reproduction steps
- Actions already tried and what changed

Start with the exact error text, status label, feature name, and UI label. Then search synonyms and the broader product area. In a docs repository, search both languages because one side may have a newer or more discoverable explanation, but answer from content verified for the current product state.

Inspect adjacent pages and navigation, especially:

- Help index, FAQs, and troubleshooting guides
- Known Issues and Release Notes
- The feature's setup or best-practice page
- Olares One guidance for hardware-specific cases
- Developer docs for CLI, chart, app publishing, and API behavior

## Turn evidence into a decision

Classify the result:

- **One verified cause**: give the applicable fix and cite it.
- **Several plausible causes**: choose the safest check that separates them; do not dump a long generic checklist.
- **Version mismatch**: state exactly which version the source covers and ask for or explain how to find the customer's version.
- **Source conflict**: show the conflict internally and escalate; do not choose whichever answer sounds more convenient.
- **No authoritative answer**: say that the cause is not yet confirmed, request the minimum evidence, and create a content/engineering gap rather than improvising.

Do not claim success merely because an operation completed. Define the user-visible or system-visible verification result.

## Citation discipline

Support each material claim with a direct link or repository file path. A source should answer the customer's actual question, not merely mention the same product. When a fix is version-specific, include the affected/fixed version in the reply. When the source has no version or verification date, surface that limitation internally.
