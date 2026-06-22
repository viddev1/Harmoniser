# Architecture

A small HTTP service used here to demonstrate the multi-tool harness. The shape is
deliberately minimal — the point is the *harness*, not the app.

## Components

| Layer        | Responsibility                                  |
|--------------|--------------------------------------------------|
| `routes/`    | HTTP boundary: validation, status codes          |
| `services/`  | Business logic and transactions                  |
| `repos/`     | Data access — the only layer that touches the DB |

Request flow: `client → route → service → repository → database`.

See the [`backend`](../skills/backend/SKILL.md) skill for the rules that enforce this,
and the [`testing`](../skills/testing/SKILL.md) skill for how each layer is tested.

## Why a shared source of truth

Three AI coding tools (Claude Code, Cursor, Codex) each expect guidance in their own
directory and format. Authoring three copies guarantees drift. Instead, everything
authored once in `.shared/` is propagated by `scripts/sync.sh`. See the top-level
[README](../../README.md) for the full data flow.
