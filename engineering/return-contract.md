# The Return Contract

How CC hands work back to the orchestrator. One file per ticket — `orchestration/handoffs/<ticket-id>-<slug>-return.md` — progressively filled across checkpoints. Always delivered file + pointer.

## Checkpoint 0 — inventory discrepancy (conditional)

Written only if CC's Step-3 inventory pass finds the brief contradicts the actual code. CC records the discrepancy and hands the orchestrator the pointer **before writing any code**. The orchestrator resolves it, updates the brief file, hands the pointer back. CC then re-reads the updated brief and proceeds.

## Checkpoint 1 — at PR open

The PR description *is* checkpoint 1. Fields:

- Commits / SHAs + what shipped
- **Architecture drift** — decided X / did Y / why (mandatory; "none" if none)
- **Files/modules touched vs the brief's predicted list** — deltas called out
- Test + quality-gate results
- Deviations from the brief
- New risks / follow-ups discovered
- Code work-time so far
- **Review findings** — the three diff-stage reviewers' output + how CC addressed each, verbatim
- **Suggested smoke checklist** — the precise steps to exercise what was built, including edge cases CC knows about

## Checkpoint 2 — after Deploy

The same file, completed:

- Deploy + migration status
- Final actual work-time

## Why two checkpoints

The orchestrator's review gate happens before merge — so the review-relevant fields must exist at PR open (checkpoint 1). Deploy status and final time only exist after Deploy (checkpoint 2). One artifact, filled in two passes — no second interface, no divergence risk.

## What the orchestrator does with it

Consumes the return file at the review gate (checkpoint 1) and at Close (checkpoint 2): updates the ticket, posts the closure comment, logs architecture drift to the drift log, appends the (estimate, actual) pair to the estimation calibration log.
