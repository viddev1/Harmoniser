---
name: commit-message
description: Draft a Conventional Commits message from the current diff.
---

# Commit message

Inspect the diff and produce a single Conventional Commits message.

Format:

```
<type>(<scope>): <summary in imperative mood, <=72 chars>

<body: what changed and why, wrapped at 72 cols — omit if trivial>
```

- `type` ∈ feat | fix | refactor | test | docs | chore | perf
- `scope` is the top-level area touched (e.g. `auth`, `api`, `sync`)
- Do not invent a ticket number. Do not add a footer unless there is a breaking change,
  in which case add `BREAKING CHANGE: <description>`.

Output only the commit message, nothing else.
