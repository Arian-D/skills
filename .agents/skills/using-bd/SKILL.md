---
name: using-bd
description: "Uses the bd (Beads) CLI for issue tracking workflows, setup, and best practices. Use when managing tasks with bd or integrating bd into agent workflows."
---

# Using bd (Beads)

Use this skill when you need to manage tasks with the `bd` CLI or set up best-practice workflows for AI agents. Follow these rules to keep bd data consistent, reduce workflow friction, and avoid common mistakes.

## Core Workflow (Agent-First)

1. **Find ready work**: `bd ready --json`
2. **Claim the task**: `bd update <id> --status in_progress --json` (or `--claim` for atomic claim)
3. **Do the work**: Implement, test, document
4. **Discover new work**: `bd create "..." -p 1 --deps discovered-from:<parent-id> --json`
5. **Close finished work**: `bd close <id> --reason "Completed" --json`
6. **Sync at session end**: `bd sync`

### Why this matters
- `bd ready` ensures you only pick unblocked issues.
- `--json` output is stable and parseable for agents.
- `bd sync` flushes JSONL and Git updates immediately (no debounce delays).

## Critical Rules for Agents

- **Never use `bd edit`**: it opens `$EDITOR`. Use `bd update` with field flags instead.
- **Always use `--json`** for automation and MCP-style workflows.
- **Always run `bd sync`** after creating/updating/closing issues to persist changes to git.
- **Always use non-interactive flags** in shell commands: `cp -f`, `mv -f`, `rm -rf`, `ssh -o BatchMode=yes`.
- **Never use emoji-style icons** (🔴🟠🟡) in CLI output; use small Unicode symbols instead: `○ ◐ ● ✓`.
- **Store AI planning docs in `history/`** (keep repo root clean).
- **Do not create markdown TODO lists** when bd is in use.

## Essential Commands

### Create Issues

```bash
bd create "Issue title" -t bug|feature|task|epic|chore -p 0-4 --json
bd create "Found bug" -t bug -p 1 --deps discovered-from:<parent-id> --json
```

### Update Issues

```bash
bd update <id> --status in_progress --json
bd update <id> --priority 1 --json
bd update <id> --title "New title" --json
bd update <id> --description "New description" --json
bd update <id> --design "Design notes" --json
bd update <id> --notes "Implementation notes" --json
bd update <id> --acceptance "Acceptance criteria" --json
```

### Close/Reopen

```bash
bd close <id> --reason "Done" --json
bd reopen <id> --reason "Reopening" --json
```

### Dependencies

```bash
bd dep add <child> <parent> --type blocks --json
bd dep add <child> <parent> --type related --json
bd dep add <child> <parent> --type parent-child --json
bd dep add <child> <parent> --type discovered-from --json
```

### Querying

```bash
bd list --status open --priority 1 --json
bd show <id> --json
bd ready --json
bd blocked --json
bd stale --days 30 --json
```

### Sync and Health

```bash
bd sync
bd info --json
bd daemons health --json
bd doctor
bd doctor --fix
```

### Dependency Tree Visualization

```bash
bd dep tree <issue-id> --direction=both
```

## Priorities and Types

- Priorities: `0` (critical) to `4` (backlog)
- Types: `bug`, `feature`, `task`, `epic`, `chore`

## Best Practices

- **Prefer `bd update --claim`** when multiple agents are pulling from `bd ready`.
- **Link discovered work** with `discovered-from` so it stays in the same repo and preserves traceability.
- **Use hierarchical IDs** for epics (`bd-a1b2.1`, `.2`, `.3`) to keep work organized.
- **Keep titles short** and descriptions specific (avoid long titles that hide in list output).
- **Use labels** sparingly for cross-cutting concerns.
- **Install git hooks** with `bd hooks install` to keep JSONL in sync on commit and merge (one-time per workspace).
- **Run `bd doctor`** to detect orphaned issues or database problems.
- **Use `bd doctor --fix`** to auto-remediate detected issues.

## Setup and Integration

### Initialize (Non-Interactive)

```bash
bd init --quiet
```

### Contributor Routing (OSS Workflows)

```bash
bd init --contributor
# or configure manually:
bd config set routing.mode auto
bd config set routing.contributor "~/.beads-planning"
bd repo add ~/.beads-planning
```

### Protected Branch / Sync Branch

```bash
bd init --branch beads-sync
# or configure manually:
bd config set sync.branch beads-sync
```

### MCP Server (Optional)

```bash
pip install beads-mcp
```

Configure MCP client:
```json
{
  "beads": {
    "command": "beads-mcp",
    "args": []
  }
}
```

## Landing the Plane (Session Completion)

**MANDATORY WORKFLOW when finishing a work session:**

1. **File remaining work** for follow-ups:
```bash
bd create "Follow-up: ..." -t task -p 2 --json
```

2. **Close finished issues**:
```bash
bd close <id> --reason "Completed" --json
```

3. **Sync all changes to git**:
```bash
bd sync
```

## Troubleshooting Quick Checks

- `bd info --json` for database path and daemon status
- `bd doctor` for detecting orphaned or stale issues
- `bd doctor --fix` for auto-remediation
- `BD_DEBUG_SYNC=1 bd sync` for sync merge debugging

## Common Pitfalls

- Running `bd edit` (interactive) inside agents — use `bd update` with flags instead.
- Forgetting `bd sync` after operations — JSONL won't be exported to git.
- Creating issues without `--json` when scripting — output becomes unparseable.
- Using interactive shell commands (`cp`, `mv`, `rm` without `-f`) — agents hang waiting for confirmation.
- Using interactive file operations (`apt-get` without `-y`) — agents hang on prompts.
- Mixing multiple install methods leading to wrong `bd` binary in PATH (`which -a bd`).

## Reference Docs

- `docs/CLI_REFERENCE.md`
- `docs/QUICKSTART.md`
- `docs/SYNC.md`
- `docs/TROUBLESHOOTING.md`
- `docs/SETUP.md`
- `AGENTS.md` and `AGENT_INSTRUCTIONS.md`
