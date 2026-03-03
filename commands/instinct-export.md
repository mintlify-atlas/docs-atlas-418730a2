---
title: /instinct-export Command
description: Export instincts to a shareable YAML format
---

# /instinct-export Command

Exports instincts to a shareable format for:
- Sharing with teammates
- Transferring to a new machine
- Contributing to project conventions

## Command Syntax

```bash
/instinct-export [options]
```

<ParamField path="--domain" type="string">
  Export only specified domain (e.g., `testing`, `security`)
</ParamField>

<ParamField path="--min-confidence" type="number">
  Only export instincts above threshold (0.0-1.0)
</ParamField>

<ParamField path="--output" type="string">
  Output file path (prints to stdout if omitted)
</ParamField>

<ParamField path="--scope" type="string" default="all">
  Export scope: `project`, `global`, or `all`
</ParamField>

## Examples

```bash
# Export all personal instincts
/instinct-export

# Export only testing instincts
/instinct-export --domain testing

# Only high-confidence instincts
/instinct-export --min-confidence 0.7

# Export to file
/instinct-export --output team-instincts.yaml

# Export current project only
/instinct-export --scope project --output project-instincts.yaml
```

## Output Format

```yaml
# Instincts Export
# Generated: 2026-03-03
# Source: personal
# Count: 12 instincts

---
id: prefer-functional-style
trigger: "when writing new functions"
confidence: 0.8
domain: code-style
source: session-observation
scope: project
project_id: a1b2c3d4e5f6
project_name: my-app
---

# Prefer Functional Style

## Action
Use functional patterns over classes.
```

## Related

- **Commands**: `/instinct-import`, `/instinct-status`, `/promote`
