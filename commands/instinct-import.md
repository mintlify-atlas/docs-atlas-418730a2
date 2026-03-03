---
title: /instinct-import Command
description: Import instincts from file or URL into project or global scope
---

# /instinct-import Command

Import instincts from local file paths or HTTP(S) URLs.

## Command Syntax

```bash
/instinct-import <file-or-url> [options]
```

<ParamField path="file-or-url" type="string" required>
  Local file path or HTTP(S) URL to instincts YAML file
</ParamField>

<ParamField path="--dry-run" type="boolean">
  Preview without importing
</ParamField>

<ParamField path="--force" type="boolean">
  Skip confirmation prompt
</ParamField>

<ParamField path="--min-confidence" type="number">
  Only import instincts above threshold
</ParamField>

<ParamField path="--scope" type="string" default="project">
  Target scope: `project` or `global`
</ParamField>

## Examples

```bash
# Import from local file
/instinct-import team-instincts.yaml

# Import from URL
/instinct-import https://github.com/org/repo/instincts.yaml

# Preview without importing
/instinct-import team-instincts.yaml --dry-run

# Import to global scope with force
/instinct-import team-instincts.yaml --scope global --force
```

## Import Process

```
📥 Importing instincts from: team-instincts.yaml
================================================

Found 12 instincts to import.

Analyzing conflicts...

## New Instincts (8)
These will be added:
  ✓ use-zod-validation (confidence: 0.7)
  ✓ prefer-named-exports (confidence: 0.65)
  ✓ test-async-functions (confidence: 0.8)
  ...

## Duplicate Instincts (3)
Already have similar instincts:
  ⚠️ prefer-functional-style
     Local: 0.8 confidence, 12 observations
     Import: 0.7 confidence
     → Keep local (higher confidence)

  ⚠️ test-first-workflow
     Local: 0.75 confidence
     Import: 0.9 confidence
     → Update to import (higher confidence)

Import 8 new, update 1?
```

## Merge Behavior

- Higher-confidence import becomes update candidate
- Equal/lower-confidence import is skipped
- User confirms unless `--force` is used

## Source Tracking

Imported instincts are marked with:
```yaml
source: inherited
scope: project
imported_from: "team-instincts.yaml"
project_id: "a1b2c3d4e5f6"
```

## Related

- **Commands**: `/instinct-export`, `/instinct-status`
