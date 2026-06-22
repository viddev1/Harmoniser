# Project conventions

General conventions that aren't specific to one skill. Authored once here in
`.shared/docs/` and referenced by both `AGENTS.md` and `CLAUDE.md`.

## Code style

- Format on save; never hand-format. CI rejects unformatted code.
- Prefer pure functions. Push side effects to the edges.
- No commented-out code on `main`. Delete it — git remembers.

## Naming

- `camelCase` for variables/functions, `PascalCase` for types, `SCREAMING_SNAKE` for consts.
- Booleans read as predicates: `isReady`, `hasAccess`, `canRetry`.

## Git

- Conventional Commits (see the `commit-message` prompt).
- One logical change per PR. If you can't summarize it in one line, split it.

## Source of truth

- Behavioral guidance for AI tools lives in `.shared/`. Do not edit the synced copies
  under `.claude/`, `.cursor/`, or `.codex/` — run `scripts/sync.sh` instead.
