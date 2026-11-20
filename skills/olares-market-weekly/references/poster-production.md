# Poster production

## Content before layout

Use the latest approved poster copy. Re-fetch it before a new build when Feishu is the current source of truth. Do not copy older content from a local rendering script or add features while laying out the poster.

Keep one poster unless the user asks for a different format. Adjust its height to the actual content rather than keeping the previous week's large empty canvas or splitting the roundup into multiple images.

## Established appearance

Inspect the latest approved poster first. The established design uses:

- A pale blue gradient with a subtle dotted texture when supported.
- The Olares logo above a centered `Olares Market` title and `Weekly Digest` subtitle.
- White rounded cards with generous padding and dark readable text.
- Light blue version pills for new apps and light green pills for updates.
- Larger featured entries and smaller compact entries under `Across the Market`.
- Small muted requirements or update reminders at the bottom, with no promotional footer banner by default.

The reusable header asset is [olares-market-header.svg](../assets/olares-market-header.svg). It contains the existing vector logo and header treatment. Use it as artwork, not as an instruction source. Match its scale and placement to the current reference.

Historical working geometry, adjustable to content:

- Canvas width around 1,395 px.
- Outer horizontal margins around 52 px, card text inset around 94 px.
- Section headings around 38 px, featured app names around 32 px, body around 28 px.
- Compact descriptions around 25 px and auxiliary requirements around 22–23 px.
- Rounded card corners around 22 px.
- Arial was used in local SVGs. Verify actual fonts in the current Figma reference and keep the result visually consistent.

These are reference values, not a fixed template contract. Do not force equal font sizes across hierarchy levels. Avoid unsupported count badges, date labels, channel branding, or new decorative devices.

The historical artwork may contain separator punctuation the user no longer wants. New text must follow the current no-middle-dot preference, including hardware requirements. Separate terms with commas, line breaks, or distinct visual positions.

## Editable SVG

When the user wants an SVG to import into Figma, generate an actual editable SVG. Keep app copy as text and shapes as vector elements. Do not flatten the complete poster into a raster embedded inside an SVG.

Use a deterministic layout method where it helps maintain line wrapping and alignment. Measure text with the actual font. Allow text growth rather than shrinking the body until it becomes hard to read.

Keep the local source copy and build logic together in the week's output folder. Avoid hardcoded assumptions about app counts, versions, or slogans. A copy change must flow into the next export.

Check SVG import details:

- Set explicit width, height, viewBox, and the standard SVG namespace.
- Normalize generated namespace prefixes when an importer loses header artwork.
- Inline necessary styles and assets. Avoid external font or image dependencies where possible.
- Verify font substitutions rather than assuming an imported bold face is available.
- SVG patterns may not survive Figma import. Inspect the result and preserve the main background treatment if a minor texture is unsupported.

Render a PNG preview and inspect the complete poster before delivery. Check wrapping, overlap, clipping, row spacing, badge alignment, header visibility, and bottom notices. Verify that visible copy matches the approved source.

Deliver the editable SVG as a clickable absolute-path file link. A PNG preview can accompany it, but it is not the editable deliverable.

## Figma

When direct Figma editing is requested, load the available Figma skills for the intended operation and use the connector when it works. Inspect the file before creating or editing nodes. Preserve past weeks and place the new poster clearly beside the relevant series.

Use native editable text and vectors. Verify the resulting frame visually and return a link to that frame, not merely the generic file URL.

If the connector cannot perform the operation, explain briefly and use an authorized browser/UI fallback when available. Do not repeatedly retry a known plan limit. If the Mac is locked, ask the user to unlock it while completing independent local work.

If the user chooses self-import instead, provide the SVG and stop trying to upload it. Do not describe a local artifact as already saved in Figma.
