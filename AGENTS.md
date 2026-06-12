# Codex Guidelines

These are global working preferences ported from the global Claude instructions.
When a Claude-specific command or skill is unavailable in Codex, preserve the
intent and use the closest Codex-native workflow.

## Operating Style

- Bias toward action. Do not stop at brainstorms, plans, or task lists unless the
  user asks for them or the task is genuinely ambiguous.
- For implementation work, prefer TDD: write or update the focused test first,
  implement the change, then run the relevant verification.
- Do work now. Do not propose deferring or scheduling work unless it cannot be
  completed in the current session because of external state.

## Planning And Parallel Work

- Optimize for implementation velocity. Decompose broad work into independent
  units and use parallel agents when the user asks for delegation/parallel work
  or the Codex environment explicitly permits it.
- Actively spot independent sidecar tasks that can run in parallel, but keep
  context-local implementation work in one agent when that improves code
  quality; do not over-parallelize tightly coupled edits.
- Keep changes that belong together within a single agent scope. Locality and
  quality beat raw concurrency when the work is cohesive.
- When the user adds another task mid-task, first decide whether it is related
  to the current work. If it is unrelated, append it to the task list; if no
  task list exists yet, create one, then continue the current task without
  switching context.
- When multiple agents will edit the same code area, isolate each in its own
  `.worktrees/` worktree to avoid merge conflicts.
- Before committing design/spec-heavy work, run the Codex `/review` command when
  practical. If `/review` is unavailable or not appropriate for the scope, use a
  dedicated subagent for code review. Do not use `codex-companion.mjs` for that
  review unless the user explicitly asks for it.
- Keep plans compact and execution-oriented.

## Dev Environment

- macOS: prefer `gsed`/`gawk` over BSD `sed`/`awk` when GNU extensions are
  needed. Prefer Homebrew bash at `/opt/homebrew/bin/bash`; system bash is 3.2.
- Always quote glob patterns passed to the shell so zsh does not expand or
  reject them before the intended command receives them.
- Linux/Docker: assume user `coder` with passwordless sudo when that environment
  is present.
- Prefer `just` and `justfile` project command surfaces over `make` and
  `Makefile` when adding or updating repo-local automation.
- Use `bun` only for JavaScript tooling. Do not use `npm`, `npx`, `pnpm`, or
  `pnpx` unless the user explicitly authorizes an exception.
- When a needed tool is missing, ask the user for permission to install it with
  the appropriate package manager (`brew`, `pip`, `npm`, etc.) instead of
  silently avoiding the tool.
- Do not create a separate project Python venv; use the global venv.

## Languages And Type Checking

- Primary languages: Python and TypeScript/Next.js frontend.
- Python: use Python 3.10+ syntax such as `list[str]` and `T | None`.
- Python typing imports: prefer importing only `Callable`, `Protocol`,
  `TypeVar`, and `Generic` from `typing` when needed.
- Python data modeling: prefer `dataclasses` or `pydantic` over plain dicts for
  structured data.
- Python tests: run `pytest`, not `python -m pytest`.
- Python logging: use lazy `%` formatting.
- Pin dependencies in `requirements.txt` when a project uses that file.

## Frontend

- Use TypeScript only. Prefer Next.js App Router and Tailwind v4 when working in
  those stacks.
- Keep source maps enabled. Do not track generated `.js` or `.map` files from
  TypeScript sources.
- For UI/UX work, use the `$impeccable` skill if installed. Otherwise follow
  Codex frontend guidance and verify WCAG 2.1 AA contrast/accessibility.
- Use design tokens for colors and contrast. Avoid hardcoded chart colors.
## Architecture

- Shift work to the backend when it reduces client complexity, such as API-level
  filtering.
- Prefer CLI/config-file workflows over GUI-only configuration.
- Use process-compose for multi-process startup orchestration by default.
- Never edit the text of a database migration file once it has been applied.
  Add a new forward migration for every schema/data repair instead.
- Do not start long-running app dev servers by default; the user generally runs
  their own dev server. If verification or platform instructions require one,
  be explicit about why, provide the URL, and leave the process state clear.
- The dev environment may not auto-reload on file changes. When code or config
  changes are ready for user testing, restart or kill affected process-compose
  components through the `pc` skill or equivalent so the next request gets a
  fresh process.
- Persist fixes in source, scripts, or config. Do not only patch the live
  environment; when deploy/setup automation misbehaves, fix the automation and
  the environment in the same pass when safe.

## Code Organization

- Keep files focused and target fewer than 200 lines. Refactor when a file grows
  past that without a strong reason.
- Maintain single responsibility per file.
- Add a file-level docstring/comment for new source files that benefits from a
  short purpose statement.
- Scripts must work regardless of the caller's current working directory.
- Scripts must exit with an error on unknown flags.

## Research

- For documentation research, use configured documentation/search MCP tools such
  as Context7 and Exa in parallel when available. Prefer official docs for
  technical facts and cite sources when answering.

## Secrets And Config

- Projects use `dotenvx` and `.env.vault` where configured. The key is expected
  at `~/.dotenvx.keys`.
- Commit plaintext non-secret `.env` files and encrypted `.env.vault` files when
  they are part of the project convention. Do not add `.env.vault` to
  `.gitignore`.
- Never default missing config values. Fail hard on missing required config.
- Never deploy with default credentials such as `admin/admin`.

## Git

- If a Codex `$commit` skill or equivalent repo workflow is available, use it for
  all staging and commits.
- If no such workflow is available, emulate the intent: inspect status and diff,
  stage only intended files, keep commits atomic, use conventional commit format
  with emoji when consistent with the repo, and commit directly to the relevant
  branch.
- Never pass `--no-verify`, `--no-review`, `--no-security-review`, or
  `--no-simplify` without explicit user approval in the same turn.
- Do not create PRs unless explicitly asked.

## Codex Plugins And Skills

- Personal Codex plugins and skills live under `~/.codex/plugins/` and
  `~/.codex/skills/` unless a repo-local plugin marketplace is configured.
- When a skill contains deterministic repeatable logic, move that logic into a
  bundled `scripts/` helper and have `SKILL.md` call the helper first. Keep prose
  for judgment and exceptions so future skill use is faster and lower-token.
- When using a skill, actively spot self-contained improvements that reduce
  repeated work or speed execution. If the improvement is low-risk, fork a
  background agent to improve that skill without asking first, while keeping the
  current user task moving.
- Do not hand-edit Codex-managed plugin caches or vendor imports unless the user
  explicitly asks for that maintenance task.
- When working on Claude plugin content, personal plugins live in
  `~/.claude/plugins/marketplaces/local/`. Treat the rest of `~/.claude/plugins/`
  as Claude Code-managed unless the user explicitly asks for maintenance there.
- For browser automation, use the `dev-browser` skill when explicitly requested
  or when persistent browser state is needed.
- If the user explicitly authorizes `dev-browser --connect` despite access to
  browser pages, cookies, and authenticated sessions, treat that as permission
  for the current session and use it only for the requested verification.
- Do not use filesystem MCP servers.

## Design Assets

- For hero photos, marketing imagery, and product mocks where no real asset
  exists, use available image-generation tooling such as the `imagegen` skill or
  configured image MCP tools.
- For voice, music, and sound effects, use ElevenLabs MCP tooling when
  available.

## Hard Rules

- Do not move `CLAUDE.md` or `AGENTS.md` files unless explicitly requested.
- Do not edit files outside the current working directory subtree unless the user
  explicitly requested that scope or path.
- Use `.worktrees/` under the project root for worktrees.
- Parallelize independent tests where practical.
- Never link private URLs such as internal, CRM, or staging URLs in public
  issues/PRs. Use placeholders like `https://your-twenty.example.com`.
- LaTeX: use TeX quotes such as ``text'' rather than `"text"`.
- German LaTeX: use `\usepackage[T1]{fontenc}` and
  `\usepackage[ngerman]{babel}`.
