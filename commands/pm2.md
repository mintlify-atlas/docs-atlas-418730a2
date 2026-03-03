---
title: /pm2 Command
description: Auto-analyze project and generate PM2 service commands
---

# /pm2 Command

Auto-analyze project and generate PM2 service commands for managing development services.

## Workflow

1. Check PM2 (install via `npm install -g pm2` if missing)
2. Scan project to identify services (frontend/backend/database)
3. Generate config files and individual command files
4. Update project CLAUDE.md with PM2 info
5. Display completion summary

## Service Detection

| Type | Detection | Default Port |
|------|-----------|-------------|
| Vite | vite.config.* | 5173 |
| Next.js | next.config.* | 3000 |
| Nuxt | nuxt.config.* | 3000 |
| CRA | react-scripts in package.json | 3000 |
| Express/Node | server/backend/api directory | 3000 |
| FastAPI/Flask | requirements.txt / pyproject.toml | 8000 |
| Go | go.mod / main.go | 8080 |

**Port Detection Priority**: User specified > .env > config file > scripts args > default port

## Generated Files

```
project/
├── ecosystem.config.cjs              # PM2 config
├── {backend}/start.cjs               # Python wrapper (if applicable)
└── .claude/
    ├── commands/
    │   ├── pm2-all.md                # Start all + monit
    │   ├── pm2-all-stop.md           # Stop all
    │   ├── pm2-all-restart.md        # Restart all
    │   ├── pm2-{port}.md             # Start single + logs
    │   ├── pm2-{port}-stop.md        # Stop single
    │   ├── pm2-{port}-restart.md     # Restart single
    │   ├── pm2-logs.md               # View all logs
    │   └── pm2-status.md             # View status
    └── scripts/
        ├── pm2-logs-{port}.ps1       # Single service logs
        └── pm2-monit.ps1             # PM2 monitor
```

## Command Syntax

```bash
/pm2
```

No arguments required - auto-detects services.

## Windows Configuration

### ecosystem.config.cjs

**Must use `.cjs` extension**

```javascript
module.exports = {
  apps: [
    // Node.js (Vite/Next/Nuxt)
    {
      name: 'project-3000',
      cwd: './packages/web',
      script: 'node_modules/vite/bin/vite.js',
      args: '--port 3000',
      interpreter: 'C:/Program Files/nodejs/node.exe',
      env: { NODE_ENV: 'development' }
    },
    // Python
    {
      name: 'project-8000',
      cwd: './backend',
      script: 'start.cjs',
      interpreter: 'C:/Program Files/nodejs/node.exe',
      env: { PYTHONUNBUFFERED: '1' }
    }
  ]
}
```

## Terminal Commands

After init:

```bash
## First time (with config file)
pm2 start ecosystem.config.cjs && pm2 save

## After first time (simplified)
pm2 start all          # Start all
pm2 stop all           # Stop all
pm2 restart all        # Restart all
pm2 start {name}       # Start single
pm2 stop {name}        # Stop single
pm2 logs               # View logs
pm2 monit              # Monitor panel
pm2 resurrect          # Restore saved processes
```

## Key Rules

1. **Config file**: `ecosystem.config.cjs` (not .js)
2. **Node.js**: Specify bin path directly + interpreter
3. **Python**: Node.js wrapper script + `windowsHide: true`
4. **Open new window**: `start wt.exe -d "{path}" pwsh -NoExit -c "command"`
5. **Minimal content**: Each command file has only 1-2 lines description + bash block

## Related

- **Commands**: `/setup-pm`
