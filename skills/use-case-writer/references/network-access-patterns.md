# Network access for external clients

Apply when a phone, computer, or other external client connects to an Olares service. Determine the protocol and supported access path before choosing a layout or copying a URL example.

## Establish the actual connection

Identify the caller's location, target service/instance, protocol, address source, port source, credentials, and required access policy. Use the current canonical guide and app configuration for the target version.

- HTTP APIs and web clients may use app entrances, local-domain access, or LarePass VPN as documented for that scenario.
- SSH, SFTP, and game protocols require their own host and port. Do not convert a web URL into a non-HTTP address or assume its entrance exposes those protocols.
- Multiple instances may have different local addresses or exported ports. Tell readers where to obtain the values for their selected instance.
- Do not add authentication-level changes, domain rewriting, or a VPN route unless the current instructions support them. Do not infer remote access from a same-LAN test.

## Reuse supported procedures

Search `docs/reusables/local-domain.md`, `docs/reusables/larepass-vpn.md`, corresponding Chinese fragments, and the current canonical local-access, private-network, entrance, and Overlay gateway guides. Verify filenames, regions, links, and applicability in the working repository.

Include an applicable region if the reader needs the procedure inline. Link a separate prerequisite or platform-specific setup. Keep the app's actual fields and instance-specific values local. Do not manufacture an include just to eliminate a short app-specific explanation.

For LarePass VPN screenshots, check the existing assets before adding placeholders:
- `/images/manual/get-started/larepass-vpn-desktop.png`
- `/images/manual/get-started/larepass-vpn-mobile.png`

For documented `.local` access, preserve the current guide's scheme and naming rules. Link Windows-specific setup where relevant instead of assuming the name resolves on every client. Do not derive URL patterns from an old screenshot alone.

## Choose a readable layout

- Use headings for separate procedures that benefit from visible, linkable sections.
- Use tabs for mutually exclusive paths when each tab can contain a complete procedure.
- Use a brief callout when networking is incidental to the main configuration task.
- Use a compact comparison table only if it helps readers choose a path. Do not repeat all of its content in subsequent tabs and callouts.

No layout is mandatory merely because a section is about connecting. For a short primary path, a direct procedure can be sufficient.

When tabs are useful, use descriptive labels and the site's existing component syntax:

```markdown
<tabs>
<template #Same-LAN>
[Complete supported LAN procedure]
</template>
<template #Remote-access>
[Complete supported remote procedure]
</template>
</tabs>
```

Use ordered steps for actions that must occur in sequence. Use a table or unordered list for parallel fields such as protocol, host, port, and username. State where each value comes from and where the command or client runs.

## Check the result

Keep a verified readiness or connection signal when needed to proceed. Give a relevant next action if it fails. Do not add a full client/network acceptance matrix to an ordinary use case.
