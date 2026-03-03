---
title: /update-codemaps Command
description: Analyze codebase structure and generate token-lean architecture documentation
---

# /update-codemaps Command

Analyze the codebase structure and generate token-lean architecture documentation.

## Process

1. **Scan Project Structure** - Identify project type, source dirs, entry points
2. **Generate Codemaps** - Create/update architecture docs
3. **Diff Detection** - Compare with previous codemaps
4. **Add Metadata** - Freshness headers
5. **Save Analysis Report** - Codemap diff summary

## Generated Codemaps

Created in `docs/CODEMAPS/` (or `.reports/codemaps/`):

| File | Contents |
|------|----------|
| `architecture.md` | High-level system diagram, service boundaries, data flow |
| `backend.md` | API routes, middleware chain, service → repository mapping |
| `frontend.md` | Page tree, component hierarchy, state management flow |
| `data.md` | Database tables, relationships, migration history |
| `dependencies.md` | External services, third-party integrations |

## Command Syntax

```bash
/update-codemaps
```

No arguments required.

## Codemap Format

Token-lean - optimized for AI context consumption:

```markdown
# Backend Architecture

## Routes
POST /api/users → UserController.create → UserService.create → UserRepo.insert
GET  /api/users/:id → UserController.get → UserService.findById → UserRepo.findById

## Key Files
src/services/user.ts (business logic, 120 lines)
src/repos/user.ts (database access, 80 lines)

## Dependencies
- PostgreSQL (primary data store)
- Redis (session cache, rate limiting)
- Stripe (payment processing)
```

## Metadata Header

```markdown
<!-- Generated: 2026-03-03 | Files scanned: 142 | Token estimate: ~800 -->
```

## Tips

- Focus on **high-level structure**, not implementation details
- Prefer **file paths and function signatures** over full code blocks
- Keep each codemap under **1000 tokens**
- Use ASCII diagrams for data flow
- Run after major feature additions or refactoring

## Related

- **Commands**: `/update-docs`
