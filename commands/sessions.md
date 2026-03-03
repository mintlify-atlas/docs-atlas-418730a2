---
title: /sessions Command
description: Manage Claude Code session history - list, load, alias, and edit sessions
---

# /sessions Command

Manage Claude Code session history stored in `~/.claude/sessions/`.

## Command Syntax

```bash
/sessions <action> [options]
```

## Actions

### List Sessions

```bash
/sessions                              # List all sessions (default)
/sessions list                         # Same as above
/sessions list --limit 10              # Show 10 sessions
/sessions list --date 2026-02-01       # Filter by date
/sessions list --search abc            # Search by session ID
```

### Load Session

```bash
/sessions load <id|alias>             # Load session
/sessions load 2026-02-01             # By date
/sessions load a1b2c3d4               # By short ID
/sessions load my-alias               # By alias name
```

### Create Alias

```bash
/sessions alias <id> <name>           # Create alias
/sessions alias 2026-02-01 today-work # Named "today-work"
```

### Remove Alias

```bash
/sessions alias --remove <name>        # Remove alias
/sessions unalias <name>               # Same as above
```

### Session Info

```bash
/sessions info <id|alias>              # Show session details
```

### List Aliases

```bash
/sessions aliases                      # List all aliases
```

## Examples

```bash
# List all sessions
/sessions list

# Create an alias for today's session
/sessions alias 2026-02-01 today

# Load session by alias
/sessions load today

# Show session info
/sessions info today

# Remove alias
/sessions alias --remove today

# List all aliases
/sessions aliases
```

## Session Storage

- Sessions stored as markdown files in `~/.claude/sessions/`
- Aliases stored in `~/.claude/session-aliases.json`
- Session IDs can be shortened (first 4-8 characters)
- Use aliases for frequently referenced sessions

## Related

- **Commands**: `/claw`
