---
title: /setup-pm Command
description: Configure your preferred package manager (npm/pnpm/yarn/bun)
---

# /setup-pm Command

Configure your preferred package manager for this project or globally.

## Detection Priority

When determining which package manager to use:

1. **Environment variable**: `CLAUDE_PACKAGE_MANAGER`
2. **Project config**: `.claude/package-manager.json`
3. **package.json**: `packageManager` field
4. **Lock file**: Presence of package-lock.json, yarn.lock, pnpm-lock.yaml, or bun.lockb
5. **Global config**: `~/.claude/package-manager.json`
6. **Fallback**: First available (pnpm > bun > yarn > npm)

## Command Syntax

```bash
node scripts/setup-package-manager.js <action> [manager]
```

## Actions

### Detect Current

```bash
node scripts/setup-package-manager.js --detect
```

### Set Global Preference

```bash
node scripts/setup-package-manager.js --global pnpm
```

### Set Project Preference

```bash
node scripts/setup-package-manager.js --project bun
```

### List Available

```bash
node scripts/setup-package-manager.js --list
```

## Configuration Files

### Global Configuration

```json
// ~/.claude/package-manager.json
{
  "packageManager": "pnpm"
}
```

### Project Configuration

```json
// .claude/package-manager.json
{
  "packageManager": "bun"
}
```

### package.json

```json
{
  "packageManager": "pnpm@8.6.0"
}
```

## Environment Variable

```bash
# macOS/Linux
export CLAUDE_PACKAGE_MANAGER=pnpm

# Windows (PowerShell)
$env:CLAUDE_PACKAGE_MANAGER = "pnpm"
```

## Related

- **Commands**: `/pm2`
