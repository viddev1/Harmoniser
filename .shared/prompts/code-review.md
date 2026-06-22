---
name: code-review
description: Review the current diff for correctness and convention adherence.
---

# Code review

Review the staged/working diff. For each finding, give: file:line, severity
(blocker / should-fix / nit), and a concrete suggested change.

Check, in order:

1. **Correctness** — logic bugs, off-by-one, unhandled errors, race conditions.
2. **Conventions** — does it follow the `backend` and `testing` skills? Flag any
   SQL outside a repository, missing input validation, or untested error branches.
3. **Tests** — does the change include tests for new behavior and regressions?
4. **Clarity** — naming, dead code, comments that lie.

End with a one-line verdict: `APPROVE`, `APPROVE WITH NITS`, or `REQUEST CHANGES`.
