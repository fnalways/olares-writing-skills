# Developer documentation conventions

Conventions specific to docs under `/docs/developer/`.

## Code examples

**YAML with line highlighting:**
```markdown
    ```yaml {5,8-10}
    key: value
    list:
      - item1
      - item2  # Line 5 highlighted
    nested:
      key1: val1
      key2: val2  # Lines 8-10 highlighted
      key3: val3
    ```
```

**Inline code with variables:**
Use `<code v-pre>{{ .Values.variable }}</code>` for template variables that should not be processed.

## Tables

Developer docs use tables extensively for field references:

```markdown
| Field | Type | Default | Required | Description |
|-------|------|---------|----------|-------------|
| `envName` | string | None | Yes | Variable name for injection |
| `default` | any | None | No | Default value if not set |
```

Table conventions:
- Use code formatting for field names: `` `fieldName` ``
- Keep descriptions concise but complete
- Use consistent column order: Field, Type, Required, Description (add Default, Options as needed)

## Architecture diagrams

Reference images for architecture docs:
```markdown
![Architecture description](/images/developer/category/filename.png)
```

## Cross-references

Developer docs often reference related technical documents:
```markdown
## Learn more

- [Installation process](installation-process.md)
- [Environment variables](environment-variables.md)
- [CLI reference](../install/cli/olares-cli.md)
```
