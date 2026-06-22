# CLAUDE.md

Claude Code-specific entry point. This file is intentionally thin: the shared guidance
lives in [`.shared/`](.shared/) and is inherited from [`AGENTS.md`](AGENTS.md).

## Inherits

Read [`AGENTS.md`](AGENTS.md) for the universal rules. Everything there applies to
Claude Code too.

## Claude Code wiring

- **Skills**: synced to [`.claude/skills/`](.claude/skills/) from `.shared/skills/`.
  Claude discovers them automatically via each `SKILL.md` frontmatter.
- **Slash commands**: [`.claude/commands/`](.claude/commands/) — generated from
  `.shared/prompts/` by the sync script (e.g. `/code-review`, `/commit-message`).
- **Subagents**: [`.claude/agents/`](.claude/agents/) — Claude-specific, authored directly.

## Source of truth — do not edit synced files

`.claude/skills/` and `.claude/commands/` are **generated**. To change behavior, edit the
original under `.shared/` and run:

```bash
./scripts/sync.sh
```

Each generated file carries a `DO NOT EDIT` banner pointing back to its source.
