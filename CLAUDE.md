# Claude Guidelines

**Bias toward action**: Start coding immediately. No brainstorm/plan/tasks unless asked.

**TDD**: When implementing, write test first. Run after to verify.

## Planning

- Optimize for implementation velocity. Actively spot parallelization opportunities and design task breakdowns to maximize parallel execution — decompose into independent units and dispatch parallel agent teams whenever tasks lack shared state or sequential dependencies.
- When multiple agents will edit the same code area, isolate each in its own `.worktrees/` worktree to avoid merge conflicts.
- Keep changes that belong together within a single agent scope — don't fragment cohesive units across agents just to parallelize. Locality and quality beat raw concurrency.
- Never offer to defer work via `/schedule` unless the task genuinely cannot be completed now (e.g., waiting on external state). Do it now.
- Review design specs with codex (`codex-companion.mjs review --wait`) before commit — catches mismatches with deployed codebase that self-review misses.
- Debug a dynamic Workflow-tool run with `/workflow-run-report` — dumps every agent's inputs/outputs, the orchestration journal, and token/time accounting.
- When the user stacks multiple asks in one turn, create/update a task list (TaskCreate/TaskUpdate) to track what's remaining — don't drop sub-asks.

## Dev Environment

- macOS: `gsed`/`gawk` over `sed`/`awk` (BSD lacks GNU extensions). Homebrew bash (`/opt/homebrew/bin/bash`) — system bash is 3.2.
- Linux (Docker): user `coder`, passwordless sudo.
- Quote all glob patterns passed to a command (`'*.tmp'`, `--name-exact '*.example'`) so the shell doesn't expand them before the command sees them.

## Languages & Type Checking

Python (primary), TypeScript/Next.js (frontend).

## Python

- 3.10+ syntax: `list[str]`, `T | None`. Import from `typing` only `Callable`/`Protocol`/`TypeVar`/`Generic`.
- `dataclasses` or `pydantic` over plain dicts.
- `pytest` not `python -m pytest`.
- Lazy `%` in logging.
- Pinned versions in requirements.txt

## Frontend

- TypeScript only. Next.js App Router. Tailwind v4.
- Source maps on. Don't track `.js`/`.map` from TS.
- All UI/UX work uses the `impeccable` skill. WCAG 2.1 AA is non-negotiable,
  design-token contrast must be verified, and chart colors must not be
  hardcoded.

## Architecture

- Shift workload to backend (e.g., API-level filtering).
- CLI config over GUI.
- Don't build/start app — user runs own dev server.
- Dev environment does **not** auto-reload on file changes. When work is ready for testing, run `/pc restart <component>` for each process-compose component affected by the code/config change so a fresh binary/bundle replaces the running one. Never use `/pc stop` for this; stop leaves the process down and the next request 502s.
- Persist fixes — never just patch the live environment. If a deploy/setup script misbehaves, fix the script *and* the environment in the same pass so the next run does it right.

## Code Organization

- Files <200 lines. Refactor on overflow.
- Single responsibility per file.
- File-level docstring describing purpose.

## Research

Documentation research: Exa + Context7 MCP in parallel.

## Secrets

All projects use **dotenvx** + `.env.vault`. Key at `~/.dotenvx.keys`. Plaintext `.env` (non-secret) and encrypted `.env.vault` (secrets) — both committed. `.envrc` (direnv) auto-loads. See `dotenvx` skill.

## Git

- **MANDATORY**: ALL git commits and `git add` operations go through the `/commit-inline` skill — no exceptions. Never run `git commit` or `git add` directly via Bash, never wrap them in subshells, never bypass. The workflow-backed `/commit` is used only when the user explicitly asks for the workflow variant.
- **Never pass `--no-verify` / `--no-review` / `--no-security-review` / `--no-simplify` to `/commit-inline` (or `/commit`) without explicit user approval in the same turn.** Default invocation runs `/lint --fix`, `/code-review`, `/simplify`, and (when user-facing surfaces touched) `security-diff-reviewer`. Skipping any of these requires a user-stated reason.
- Don't create PRs — commit directly to the relevant branch (usually `main`, but whatever branch the work belongs on).

## Plugins

Personal plugins live in `~/.claude/plugins/marketplaces/local/`. Everything else under `~/.claude/plugins/` is Claude Code-managed — no hand-edit. Local marketplace edits go live on `/reload-plugins` (hooks need full session restart). See `plugin-dev:*` skills.


## Web Access

Use /dev-browser skill.

## Design Assets

Image generation: gemini nano banana MCP. Use for hero photos, marketing imagery, product mocks when no real asset exists.

Audio generation: ElevenLabs MCP. Use for voice, music, and sound effects.

## Hard Rules

- CLAUDE.md files must not be moved.
- **bun only** — never npm/npx/pnpm/pnpx.
- **Never default config values** — fail hard on missing config.
- **Commit both `.env` and `.env.vault`** — never `.gitignore` `.env.vault`.
- Never separate Python venv — global venv only.
- No filesystem MCP.
- Scripts work regardless of CWD.
- Keep logs (and writeable runtime dirs) outside the source tree — in-tree writes trip dev file watchers (e.g. Turbopack Fast Refresh loop).
- Exit error on unknown `--flags`.
- Worktrees in `.worktrees/` relative to project root.
- Parallelize tests.
- Never edit files outside CWD subtree.
- Never deploy with default credentials (e.g., Grafana admin/admin).
- Never link private URLs (internal/CRM/staging) in public issues/PRs — use placeholders like `https://your-twenty.example.com`.
- Never copy source code to a remote machine without explicit permission — this includes deploy flows that rsync/sync the working tree to a server. Confirm first.
- EAS/Expo builds upload only the strictly relevant subset — add an `.easignore` allowlist so monorepo cloud builds don't ship unrelated trees (backend, infra, docs, sibling-app media).
- LaTeX: TeX quotes (` ``text'' `) not `"text"`. German LaTeX: `\usepackage[T1]{fontenc}` + `\usepackage[ngerman]{babel}`.
