# Harmoniser — multi-tool AI harness

A demonstration harness that lets **Claude Code, Cursor, and Codex** share one set of
skills, prompts, and docs without drift. Everything is authored once in **`.shared/`**
and propagated into each tool's native directory by **`scripts/sync.sh`**.

## Data flow

```
                       .shared/   (SOURCE OF TRUTH — edit here)
                       ├── skills/      backend/SKILL.md, testing/SKILL.md
                       ├── prompts/     code-review.md, commit-message.md
                       └── docs/        architecture.md, conventions.md
                              │
              ./scripts/sync.sh  (propagate — idempotent, manifest-tracked)
                              │
        ┌─────────────────────┼─────────────────────┐
        ▼                     ▼                     ▼
   .claude/               .cursor/               .codex/
   ├── skills/   ◀syncd   ├── skills/   ◀syncd   ├── skills/   ◀syncd
   ├── commands/ ◀gen     ├── commands/ ◀gen     ├── prompts/  ◀gen
   └── agents/   authored ├── rules/    ◀gen     └── agents/   authored
                          └── commands/ ◀gen
```

`◀syncd` = copied verbatim · `◀gen` = generated/transformed · `authored` = per-tool, hand-written

## Entry points

- `AGENTS.md` — universal instructions (Codex + any AGENTS.md-aware tool)
- `CLAUDE.md` — Claude Code entry point; inherits from `AGENTS.md`

## Usage

```bash
./scripts/sync.sh          # propagate .shared/ into all three tools
./scripts/sync.sh --check  # CI gate: fails if any tool is out of date
./scripts/sync.sh --help
```

## Rules of the road

1. **Edit only `.shared/`.** Every generated file carries a `DO NOT EDIT` banner.
2. Run `./scripts/sync.sh` after changing anything in `.shared/`.
3. Wire `./scripts/sync.sh --check` into CI so a stale tool dir fails the build.
4. Tool-specific *agents* are authored directly (formats differ); only skills and
   prompts are synced.

## What's generated vs. tracked

`scripts/sync.sh` records every file it produces in `.sync-manifest`. Deleting a skill
or prompt from `.shared/` and re-running the sync prunes the corresponding generated
files everywhere. You may either commit the generated dirs (so non-syncing teammates
get them) or gitignore them and rely on `--check` in CI — both are valid.
