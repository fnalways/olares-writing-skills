# Network access for external clients (LAN vs VPN)

**When to apply**: Any time the use case involves a client app running **outside Olares** (phone app, desktop app, browser on another computer) connecting to an Olares-hosted service. Proactively detect this from the user's input and apply the appropriate pattern below.

## Choosing between Tabs and Callout

- **Use Tabs** when the section's primary purpose is **establishing the connection**. The reader needs a complete walkthrough covering network setup, entering the address, and verifying connectivity. The connection itself is the problem this section solves.
  - Example: Krita's "Connect Krita to ComfyUI" (`comfyui-for-krita.md`).

- **Use Callout** when the section's primary purpose is **configuring the client app**, and the network address is just one field among many. The reader's focus is on getting the app set up, not on network connectivity.
  - Example: OpenCode's "Configure the connection" (`opencode.md`), Context7's "Connect external clients via MCP" (`context7.md`).

**Simple test**: If the section is "how to connect", use tabs. If the section is "how to configure/set up", and the URL is one step in a larger procedure, use a callout.

## Tabs pattern

Use tab labels `#Use-.local-domain-(LAN)` and `#Use-.com-domain-(VPN)`.

### LAN tab template

User is on the same local network. Use the `.local` domain and `http`. No authentication level change or VPN needed.

Always include the Windows users callout after the intro sentence:

```markdown
:::info Windows users
On Windows, multi-level `.local` domains require additional setup. Try one of these:
- **Import hosts in LarePass**: Open the LarePass desktop app and use the built-in option to import Olares hosts to your system.
- **Use the single-level domain**: Change `https://806ba3e40.{username}.olares.com` to `http://806ba3e40-{username}-olares.local`.

For details, see [Access Olares services locally](../manual/best-practices/local-access.md).
:::
```

For the URL conversion step, use the established pattern:

```markdown
2. For **Host address**, use your [App] URL with the `.local` domain and `http`. For example, if your [App] URL is:
    ```plain
    https://abc123.{username}.olares.com
    ```
    Change it to:
    ```plain
    http://abc123.{username}.olares.local
    ```
```

Do NOT use `"becomes"` or `"Change X to Y and A to B"` for URL conversions. Always use `"For example, if your URL is: ... Change it to: ..."`.

### VPN tab template

User is on a different network. Requires updating the authentication level and enabling LarePass VPN. Structure:

1. A high-level step describing the access policy change (e.g., "Update [App]'s access policy to enable direct access from external apps:"), with sub-steps (a. b.) for the specific navigation and action. Bold the UI control name: **Authentication level**.
2. A step for enabling LarePass VPN. This is a **single step**, not a separate H3 section. Reuse the existing LarePass VPN screenshot (`/images/manual/get-started/larepass-vpn-mobile.png` for mobile, `/images/manual/get-started/larepass-vpn-desktop.png` for desktop) instead of creating placeholders.
3. Remaining connection steps.

### Connection detail steps

When entering server connection info, make each field its own numbered step rather than bundling them in an unordered list under a single "Enter the connection details" step. For example: one step for **Host address**, one step for username and password. This keeps each action distinct and scannable.

## Callout pattern

Use when the connection is just one step in a larger client configuration.

The main steps use VPN + `.com` domain as the default path. Add a `:::tip` callout right after the VPN step to mention the `.local` alternative. Link to the best practices page for platform-specific details (including Windows) instead of inlining them.

```markdown
1. Enable LarePass VPN on your computer to connect to Olares.
   ![Enable LarePass VPN on desktop](/images/manual/get-started/larepass-vpn-desktop.png#bordered)

   :::tip On the same local network?
   If your computer and Olares are on the same LAN, you can skip VPN and use the `.local` domain instead. Replace `https://{hash}.{username}.olares.com` with `http://{hash}.{username}.olares.local` in the config below. For details, see [Access Olares services locally](../manual/best-practices/local-access.md).
   :::

2. [Next configuration step using the .com URL...]
```
