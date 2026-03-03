---
title: /update-docs Command
description: Sync documentation with the codebase, generating from source-of-truth files
---

# /update-docs Command

Sync documentation with the codebase, generating from source-of-truth files.

## Sources of Truth

| Source | Generates |
|--------|----------|
| `package.json` scripts | Available commands reference |
| `.env.example` | Environment variable documentation |
| `openapi.yaml` / route files | API endpoint reference |
| Source code exports | Public API documentation |
| `Dockerfile` / `docker-compose.yml` | Infrastructure setup docs |

## Process

1. **Identify Sources** - Find source-of-truth files
2. **Generate Script Reference** - Extract commands from package.json
3. **Generate Environment Docs** - Extract variables from .env.example
4. **Update Contributing Guide** - Development setup and procedures
5. **Update Runbook** - Deployment and operations
6. **Staleness Check** - Flag docs not modified in 90+ days
7. **Show Summary** - Report what was updated

## Command Syntax

```bash
/update-docs
```

No arguments required.

## Example Output

```
Documentation Update
──────────────────────────────
Updated:  docs/CONTRIBUTING.md (scripts table)
Updated:  docs/ENV.md (3 new variables)
Flagged:  docs/DEPLOY.md (142 days stale)
Skipped:  docs/API.md (no changes detected)
──────────────────────────────
```

## Generated Sections

### Script Reference

```markdown
| Command | Description |
|---------|-------------|
| `npm run dev` | Start development server with hot reload |
| `npm run build` | Production build with type checking |
| `npm test` | Run test suite with coverage |
```

### Environment Variables

```markdown
| Variable | Required | Description | Example |
|----------|----------|-------------|---------|  
| `DATABASE_URL` | Yes | PostgreSQL connection string | `postgres://user:pass@host:5432/db` |
| `LOG_LEVEL` | No | Logging verbosity (default: info) | `debug`, `info`, `warn`, `error` |
```

## Rules

- **Single source of truth**: Always generate from code
- **Preserve manual sections**: Only update generated sections
- **Mark generated content**: Use `<!-- AUTO-GENERATED -->` markers
- **Don't create docs unprompted**: Only create new files if explicitly requested

## Related

- **Commands**: `/update-codemaps`
