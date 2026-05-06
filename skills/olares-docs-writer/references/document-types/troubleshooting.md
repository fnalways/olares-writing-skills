# Troubleshooting documentation

Problem-solution guides that help users diagnose and resolve issues efficiently.

## Key characteristics

- **Problem-focused**: Clear symptom identification.
- **Root cause analysis**: Explains why the issue occurs.
- **Actionable solutions**: Step-by-step fixes with verification.
- **Multi-platform support**: Separate sections for macOS/Windows when applicable.

## Standard format

```markdown
---
outline: [2, 3]
description: Brief description of the problem and solution.
---

# Problem title (e.g., "VPN not connecting")

Use this guide when [brief description of when to use this guide].

## Condition

**macOS** (if platform-specific)
- Symptom 1
- Symptom 2

**Windows** (if platform-specific)
- Symptom 1
- Symptom 2

## Cause

Explanation of why this problem occurs. Include technical context when helpful.

- **Cause category 1**: Description
- **Cause category 2**: Description

## Solution

### Platform-specific solution (e.g., "macOS")

Brief overview of the fix.

:::info
Optional note about platform variations or prerequisites.
:::

1. First step with UI element references in **bold**.
   ![Screenshot description](/images/manual/help/filename.png#bordered){width=70%}

2. Second step with code/command if applicable:
   ```bash
   command --example
   ```

3. Final step with verification.

### Alternative platform solution (e.g., "Windows")

[Repeat structure for other platforms]

## Prevention (Optional)

Tips to avoid this issue in the future.
```

## Section guidelines

- **Title**: Describe the *problem* or *error message*, not the solution. Keep it concise (5-8 words). Use quotes for error messages: `"System error" in LarePass`. Examples: `VPN not connecting`, `Memory not freed after stopping apps`.
- **Condition**: List specific symptoms that indicate this guide applies. Observable user-facing problems, error messages in **bold**, platform-specific symptoms under platform headings (`**macOS**`, `**Windows**`).
- **Cause**: Explain the underlying reason. Technical but accessible. Link to related concepts. List multiple causes as bullets when applicable.
- **Solution**: Use platform sections (`### macOS`, `### Windows`) when needed. Numbered steps with UI elements in **bold**, code blocks for commands, screenshots for complex UI, verification steps. Include admonitions: `:::info` (prerequisites/context), `:::tip` (shortcuts), `:::warning` (cautions).
- **Prevention** (optional): Tips to avoid the issue.

## File naming and location

Troubleshooting docs use the `ts-` prefix:
- `ts-larepass-vpn-not-working.md`
- `ts-network-not-ready.md`
- `ts-system-error.md`

Location:
- English: `/docs/manual/help/`
- Chinese: `/docs/zh/manual/help/`

## Complex troubleshooting

For issues requiring diagnostic information gathering, use step-based diagnostics:

```markdown
### Step 1: Identify the failing pod

Check the status of system pods.

1. Run command:
   ```bash
   kubectl get pods -A
   ```
2. Check output for pods not in `Running` state.

### Step 2: Inspect the pod error

View detailed error messages.

### Step 3: Contact support

Create an issue with the information gathered.
```
