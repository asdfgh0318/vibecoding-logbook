# VIBECODING

Workspace for projects built with Claude Code, plus an automated work logging system.

## Directory Structure

```
VIBECODING/
├── [PROJECTS]
│   ├── bdmenu_ada/        # Categorized app launcher
│   ├── settings-tools/    # i3 settings tools
│   ├── symulator_fpv/     # FPV drone simulator
│   ├── zegarek_google/    # Google watch doom emacs setup
│   ├── suspend_macbook/   # MacBook suspend scripts
│   └── adam_laptop/       # Laptop config
│
├── [LOGGING SYSTEM]
│   ├── WORK_LOGS          # Today's work (commits + progress)
│   ├── archive/           # Previous days (auto-archived)
│   ├── generate-log.sh    # Daily log generator
│   ├── log.sh             # Quick progress notes
│   ├── check.sh           # Check uncommitted work
│   ├── commit-all.sh      # Quick commit everything
│   └── backfill.sh        # Generate logs for past days
│
├── [TRASH - CAN DELETE]
│   ├── days/              # Old logging structure
│   ├── index.md           # Old logging structure
│   ├── screenshots/       # Old logging structure
│   └── session-logger.sh  # Old auto-hook (replaced by manual log)
│
└── [PERSONAL FILES]
    └── doom-cheatsheet.org
```

---

## Work Logging System

### How It Works

1. **Daily at 11pm** (via cron): `generate-log.sh` runs
   - Archives yesterday's WORK_LOGS to `archive/YYYY-MM-DD.md`
   - Creates fresh WORK_LOGS with today's commits from all projects

2. **During sessions**: You or Claude runs `log "what was done"`
   - Appends timestamped progress notes to WORK_LOGS

3. **End of session**: Run `vcheck` to see uncommitted work
   - Paste output to Claude for proper commit messages
   - Or run `vcommit` for quick "WIP" commits

### Shell Commands

| Command | Description |
|---------|-------------|
| `log "message"` | Add progress note to today's log |
| `vcheck` | Show all uncommitted work across projects |
| `vcommit` | Quick commit everything (WIP messages) |

### Scripts

| Script | Purpose |
|--------|---------|
| `generate-log.sh` | Creates daily WORK_LOGS, archives old ones |
| `log.sh` | Appends progress notes with timestamp |
| `check.sh` | Scans all repos for uncommitted changes |
| `commit-all.sh` | Commits all changes with "WIP: date" message |
| `backfill.sh` | Generate logs for past N days |

### WORK_LOGS Format

```markdown
# WORK LOG - 2026-01-08

## Commits (3)

### settings-tools (2)
- [1ef842b] Update README with screenshots
- [9319bee] Initial commit: settings tools for i3

### bdmenu_ada (1)
- [e8f4afb] Initial commit: categorized app launcher

## Progress

- **14:30** Created automated WORK_LOGS system
- **14:50** Added log command for quick notes
- **15:10** Added check.sh to verify commits
```

---

## End of Session Workflow

```bash
# 1. Check what's uncommitted
vcheck

# 2. Either:
#    a) Paste output to Claude for proper commits
#    b) Quick commit everything
vcommit

# 3. Generate fresh log (optional, cron does this at 11pm)
./generate-log.sh
```

---

## Setup

```bash
# Make scripts executable
chmod +x ~/ŻYCIE/VIBECODING/*.sh

# Add commands to shell (already in .bashrc)
source ~/.bashrc

# Set up daily cron (11pm)
(crontab -l; echo "0 23 * * * ~/ŻYCIE/VIBECODING/generate-log.sh") | crontab -
```

---

## Cleanup (Optional)

Remove old/unused files:

```bash
cd ~/ŻYCIE/VIBECODING
rm -rf days/ screenshots/ index.md session-logger.sh
```

---

## License

MIT
