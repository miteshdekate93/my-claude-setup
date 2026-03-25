# my-claude-setup

One-command setup to restore your full Claude Code configuration on any new machine.

Installs:
- `~/.claude/settings.json` — voice, ECC marketplace, plugins
- `~/.claude/rules/` — 9 rule files (agents, coding style, git workflow, testing, security, etc.)
- `CLAUDE.md` — project workflow instructions (written to current directory)
- `tasks/todo.md` and `tasks/lessons.md` — task tracking files (written to current directory)

---

## How To Use

### On Mac/Linux

```bash
bash setup.sh
```

### On Windows

1. Open PowerShell as Administrator
2. Allow local scripts to run (one-time):
   ```powershell
   Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
   ```
3. Run the setup:
   ```powershell
   .\setup.ps1
   ```

After running either script, restart Claude Code.

---

## What Gets Created

| Path | Description |
|------|-------------|
| `~/.claude/settings.json` | Global Claude Code settings |
| `~/.claude/rules/agents.md` | Agent orchestration rules |
| `~/.claude/rules/coding-style.md` | Immutability, file org, error handling |
| `~/.claude/rules/development-workflow.md` | Research → plan → TDD → review pipeline |
| `~/.claude/rules/git-workflow.md` | Commit format and PR process |
| `~/.claude/rules/hooks.md` | Hook types and TodoWrite practices |
| `~/.claude/rules/patterns.md` | Repository pattern, API response format |
| `~/.claude/rules/performance.md` | Model selection, context window, plan mode |
| `~/.claude/rules/security.md` | Security checklist and response protocol |
| `~/.claude/rules/testing.md` | TDD workflow, 80% coverage requirement |
| `./CLAUDE.md` | Project-level workflow instructions |
| `./tasks/todo.md` | Task tracking |
| `./tasks/lessons.md` | Lessons learned log |
