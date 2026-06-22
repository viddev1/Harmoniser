# AGENTS.md

Shared instructions for any agentic coding tool (Codex and the universal fallback for
tools that read `AGENTS.md`). Claude Code reads [`CLAUDE.md`](CLAUDE.md), which points
back here.

## Read this first

This repository keeps all behavioral guidance in **`.shared/`** — a single source of
truth — and propagates it into each tool's native directory with `scripts/sync.sh`.

- **Skills** (how to do specific work): [`.shared/skills/`](.shared/skills/)
  - [`backend`](.shared/skills/backend/SKILL.md) — API/service/repo conventions
  - [`testing`](.shared/skills/testing/SKILL.md) — how to write and structure tests
- **Reusable prompts**: [`.shared/prompts/`](.shared/prompts/)
- **Docs**: [`.shared/docs/`](.shared/docs/) — architecture, conventions

When working as Codex, the synced copies under [`.codex/skills/`](.codex/skills/) and
[`.codex/prompts/`](.codex/prompts/) are equivalent — but **edit only the originals in
`.shared/`** and re-run the sync.

## Golden rules

1. Follow the relevant skill before writing code. If a skill conflicts with a request,
   surface the conflict.
2. Never edit a synced/generated file. The header of every generated file says so.
3. Conventions live in [`.shared/docs/conventions.md`](.shared/docs/conventions.md).

## Keeping tools in sync

```bash
./scripts/sync.sh          # propagate .shared/ -> .claude .cursor .codex
./scripts/sync.sh --check  # CI: fail if any tool is out of date
```
