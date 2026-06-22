---
name: testing
description: How to write and structure tests in this project — unit vs integration boundaries, naming, fixtures, and what must be covered. Use when adding tests, fixing a flaky test, or reviewing test coverage.
version: 1.0.0
---

# Testing conventions

Single source of truth in `.shared/skills/testing/`. Synced into each tool's
`skills/` directory by `scripts/sync.sh` — edit here, never the copies.

## The pyramid

- **Unit** (most): pure functions and services with repositories mocked. Fast, no I/O.
- **Integration** (some): route → service → real test database. One per critical path.
- **End-to-end** (few): only the top user journeys.

## Naming

- File: `<subject>.test.<ext>` next to the code it tests.
- Test name reads as a sentence: `it("rejects a withdrawal larger than the balance")`.
- Group by behavior, not by method name.

## Rules

- One assertion *concept* per test. Multiple `expect`s are fine if they check one behavior.
- No shared mutable state between tests. Build fresh fixtures per test.
- Never assert on log output or sleep-based timing. Use fake timers.
- A bug fix lands with a regression test that fails before the fix.

## What must be covered

- Every error branch of a service method.
- Boundary values for any numeric or length-limited input.
- Auth: at least one "forbidden" and one "allowed" case per protected route.

## Checklist

- [ ] New code has unit tests for happy path + each error branch
- [ ] Critical paths have one integration test
- [ ] Tests pass deterministically (run twice locally)
