---
name: backend
description: Conventions for building HTTP API endpoints, services, and data access in this project. Use when adding routes, writing service logic, touching the database layer, or reviewing backend code.
version: 1.0.0
---

# Backend conventions

Authoritative guidance for backend work. This file lives in `.shared/skills/backend/`
and is the **single source of truth** — it is synced verbatim into `.claude/skills/`,
`.cursor/skills/`, and `.codex/skills/`. Never edit the synced copies.

## Layering

Keep a strict three-layer flow. Calls only ever go downward:

```
route (HTTP)  ->  service (business logic)  ->  repository (data access)
```

- **Routes** parse/validate input, call exactly one service method, and shape the response.
  No business logic, no SQL.
- **Services** own business rules and transactions. They never touch `req`/`res`.
- **Repositories** are the only place that talks to the database. Return domain objects,
  never raw rows.

## Errors

- Throw typed errors (`AppError` subclasses), never bare strings.
- Map errors to HTTP status codes in one place: the error-handling middleware.
- A 5xx must be logged with a correlation id; a 4xx must not be logged as an error.

## Validation

- Validate every external input at the route boundary with a schema (zod/pydantic-style).
- Treat anything past the boundary as trusted and typed — do not re-validate downstream.

## Checklist before opening a PR

- [ ] New endpoint has input validation and a typed error path
- [ ] No SQL outside a repository
- [ ] Service methods are unit-testable without an HTTP server
- [ ] Logs include a correlation id on the error path
