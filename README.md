# Claude Code Harness Template

A drop-in **development harness** for working with [Claude Code](https://claude.com/claude-code)
(and the [`superpowers`](https://github.com/obra/superpowers) plugin) on any repo.

It encodes one repeatable loop — **brainstorm → spec → issue → worktree → TDD →
verify → review → PR** — and wraps it in two slash commands so an agent (or you)
can drive a change end-to-end without improvising the process.

> This template was extracted from a real multi-project repo. The project-specific
> bits (project names, issue-tracker IDs, test commands) have been replaced with
> `<placeholders>`. Fill them in once and the workflow is yours.

## What's in here

| File | What it is |
|---|---|
| [`CLAUDE.md`](CLAUDE.md) | Project instructions Claude Code reads first. Edit the project table + commands. |
| [`HARNESS.md`](HARNESS.md) | The TDD loop in detail — the *how* of every stage. |
| [`AGENTS.md`](AGENTS.md) | The *why* of worktrees, specs, and issue tracking. |
| [`.claude/commands/task-init.md`](.claude/commands/task-init.md) | `/task-init` — brainstorm → local spec → file issue(s). |
| [`.claude/commands/task-implement.md`](.claude/commands/task-implement.md) | `/task-implement` — worktree → TDD → verify → review → PR. |
| [`.claude/commands/harness-setup.md`](.claude/commands/harness-setup.md) | `/harness-setup` — choose tracker, write `.claude/tracker.md` (offline). |
| [`.claude/tracker.md`](.claude/tracker.md) | Tracker config (single source of truth). Written by `/harness-setup`. |
| [`.gitignore`](.gitignore) | Ignores the local-only spec workspace and agent worktrees. |

## The loop

```
brainstorm ─▶ spec ─▶ issue(s) ─▶ worktree ─▶ TDD ─▶ verify ─▶ review ─▶ PR
  (skill)    (local)  (tracker)  (gitignored) (R/G/R) (skill)  (skill)
└─────────── /task-init ──────┘  └──────────── /task-implement ───────────┘
```

- **Specs and plans stay local** under `docs/superpowers/` (gitignored). The
  durable record is the code, the tracked issue, and the PR — never the scratch spec.
- **Implementation always happens in a worktree** under `.worktrees/`
  (gitignored), never in the main checkout.
- **Issues live in your tracker** (Plane, Linear, GitHub Issues, …), not in local files.

## Use it

1. Click **Use this template** on GitHub (or copy these files into your repo).
2. Run `/harness-setup` (choose tracker, default Plane) — writes `.claude/tracker.md`.
3. Make sure Claude Code has the `superpowers` plugin and, optionally, an MCP
   server for your issue tracker.
4. Run `/task-init <idea>` to start a task, then `/task-implement <ISSUE-ID>`.

## Placeholders to fill in

Search the repo for these remaining placeholders and replace them with your specifics (tracker coordinates are handled separately — see below):

| Placeholder | Replace with | Appears in |
|---|---|---|
| `<project>` / `<project-a>` | Your sub-project directory name(s) | `CLAUDE.md`, `HARNESS.md`, `AGENTS.md`, commands |
| `<test command>` | How you run that project's tests (e.g. `uv run pytest`) | `CLAUDE.md`, `HARNESS.md` |
| `<run command>` | How you run the project | `CLAUDE.md` |

**Tracker coordinates** (formerly `<TRACKER>`, `<PROJECT-CODE>`, `<PROJECT_ID>`, `<tracker_mcp>`) are no longer edited by hand — run `/harness-setup` to choose your tracker and write `.claude/tracker.md`.

If you only have one project (a single script or package), drop the per-project
table and the parallel-agents section entirely — the harness works for a single
project too.

## License

[MIT](LICENSE) — do whatever you like with it.
