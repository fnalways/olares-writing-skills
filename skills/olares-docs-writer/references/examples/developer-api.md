# Example: Developer documentation (API reference)

```markdown
---
outline: [2, 4]
description: Declare and validate app configuration via envs in OlaresManifest.yaml.
---

# Declarative environment variables

Use `envs` in `OlaresManifest.yaml` to declare the configuration parameters, such as passwords, API endpoints, or feature flags.

## Variable sources

Declarative variables can obtain values from configurations managed outside the application:

- **System variables**: Environment variables defined at the Olares cluster level.
- **User variables**: Environment variables defined at the Olares user level.

## Map environment variables

The following example maps the system variable `OLARES_SYSTEM_CDN_SERVICE` to an application variable `APP_CDN_ENDPOINT`:

1. In `OlaresManifest.yaml`, declare an app variable:

    ```yaml {5}
    olaresManifest.version: '0.10.0'
    olaresManifest.type: app

    envs:
      - envName: APP_CDN_ENDPOINT
        required: true
        valueFrom:
          envName: OLARES_SYSTEM_CDN_SERVICE
    ```

2. In your Helm template, reference the app variable:

    ```yaml
    env:
      - name: CDN_ENDPOINT
        value: "{{ .Values.olaresEnv.APP_CDN_ENDPOINT }}"
    ```

## Declaration fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `envName` | string | Yes | Variable name for template reference |
| `default` | any | No | Default value at authoring time |
| `valueFrom` | object | No | Maps to system/user variable |
| `required` | bool | No | Must have value to install |
| `editable` | bool | No | Can be modified after installation |

### options

Restricts the variable to a fixed list of allowed values:

```yaml
envs:
  - envName: VERSION
    options:
      - title: "Windows 11 Pro"
        value: "iso/Win11.iso"
```

## Variable references

### System environment variables

| Variable | Type | Default | Description |
|----------|------|---------|-------------|
| `OLARES_SYSTEM_CDN_SERVICE` | url | `https://cdn.olares.com` | CDN endpoint |
| `OLARES_SYSTEM_ROOT_PATH` | string | `/olares` | Olares root directory |
```
