---
title: /claw Command
description: Start the NanoClaw agent REPL with persistent conversation history
---

# /claw Command

Start an interactive AI agent session that persists conversation history to disk and optionally loads ECC skill context.

## Usage

```bash
node scripts/claw.js
```

Or via npm:

```bash
npm run claw
```

## Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `CLAW_SESSION` | `default` | Session name (alphanumeric + hyphens) |
| `CLAW_SKILLS` | *(empty)* | Comma-separated skill names to load as system context |

## REPL Commands

Inside the REPL:

```
/clear      Clear current session history
/history    Print full conversation history
/sessions   List all saved sessions
/help       Show available commands
exit        Quit the REPL
```

## How It Works

1. Reads `CLAW_SESSION` env var to select a named session
2. Loads conversation history from `~/.claude/claw/{session}.md`
3. Optionally loads ECC skill context from `CLAW_SKILLS` env var
4. Enters blocking prompt loop
5. Responses appended to session file for persistence

## Session Storage

Sessions are stored as Markdown files in `~/.claude/claw/`:

```
~/.claude/claw/default.md
~/.claude/claw/my-project.md
```

Each turn is formatted as:

```markdown
### [2025-01-15T10:30:00.000Z] User
What does this function do?
---
### [2025-01-15T10:30:05.000Z] Assistant
This function calculates...
---
```

## Examples

```bash
# Start default session
node scripts/claw.js

# Named session
CLAW_SESSION=my-project node scripts/claw.js

# With skill context
CLAW_SKILLS=tdd-workflow,security-review node scripts/claw.js
```

## Related

- **Commands**: `/sessions`
