# my-claude-setup

One-command setup to restore your full Claude Code configuration on any new machine.

Installs:
- `~/.claude/settings.json` — voice, ECC marketplace, plugins
- `~/.claude/rules/` — 11 rule files (agents, coding style, git workflow, testing, security, caveman, archon)
- `~/.claude/commands/task.md` — `/task` slash command (full autonomous pipeline)
- `CLAUDE.md` — project workflow instructions (written to current directory)
- `tasks/todo.md` and `tasks/lessons.md` — task tracking files (written to current directory)
- Archon CLI — automatic workflow engine for implement/fix/build tasks
- `~/.archon/config.yaml` — Archon config pointing to Claude binary

---

## After Running setup.sh: One-Time Auth (optional but recommended)

`setup.sh` does not require GitHub auth. But for full automation (auto push + PR creation), run once after setup:

```bash
gh auth login
# Choose: GitHub.com → HTTPS → Login with a web browser
```

**Without `gh auth login`:** `/task` still does all code work — plans, creates a local branch, writes tests, implements, reviews. At the end it outputs the exact git commands to push and create the PR manually.

**With `gh auth login`:** `/task` dispatches to Archon which handles push + PR creation autonomously.

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
| `~/.claude/rules/caveman.md` | Always-on token compression (~65% fewer tokens, auto-active) |
| `~/.claude/rules/archon.md` | Auto-dispatch implement/fix/build requests to Archon workflows |
| `~/.claude/commands/task.md` | `/task` — full pipeline: plan → TDD → implement → review → security |
| `~/.archon/config.yaml` | Archon config pointing to Claude binary |
| `./CLAUDE.md` | Project-level workflow instructions |
| `./tasks/todo.md` | Task tracking |
| `./tasks/lessons.md` | Lessons learned log |

---

## How It Works

### Token Compression (Caveman — always on)

Every Claude response is automatically compressed ~65% by dropping filler words, articles, and pleasantries while keeping full technical accuracy. Code, commits, and PRs are written normally — only prose is compressed. Longer sessions, lower cost, faster responses.

Switch modes with `/caveman lite`, `/caveman full`, `/caveman ultra`. Stop with "normal mode".

### `/task` — One Command for Everything

```
/task implement user authentication with JWT
/task fix bug in the payment module
/task refactor the database layer to use repository pattern
/task fix issue #42
/task review PR #17
```

`/task` classifies the request and routes automatically:

| Request type | What happens |
|-------------|-------------|
| New feature / implement / build | Archon `archon-piv-loop` dispatched in background → creates PR |
| Fix bug / fix issue #N | Archon `archon-fix-github-issue` dispatched in background → creates PR |
| Review PR #N | Archon `archon-smart-pr-review` dispatched in background |
| Refactor / simple fix | Inline: plan → TDD → implement → code-review → security check |
| Question / explain | Answered directly, no pipeline |

---

### Auto Workflow Engine (Archon)

When you say "implement X", "fix bug in Y", or "refactor Z", Claude automatically:
1. Detects the intent
2. Selects the right Archon workflow (idea-to-pr, fix-issue, refactor-safely, etc.)
3. Runs it in an isolated git worktree in the background
4. Reports back when done with a PR ready to merge

No manual steps. Claude handles plan → implement → validate → PR autonomously.

**Supported triggers:**
- `"implement X"` / `"build X"` → `archon-idea-to-pr`
- `"fix issue #N"` / `"fix bug in X"` → `archon-fix-github-issue`
- `"refactor X"` → `archon-refactor-safely`
- `"review PR #N"` → `archon-comprehensive-pr-review`
