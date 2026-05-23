# Conventions

## Commit

- CC is sole committer of code + `docs/`. The orchestrator commits `orchestration/` only. The orchestrator never commits source code.
- Conventional Commits: `type(scope): <ticket-id> summary`.
- Commits as the work naturally divides; multiple per ticket is fine; every commit carries the ticket ID.

| Type | Meaning |
|---|---|
| `feat` | A new feature or user-facing capability |
| `fix` | A bug fix — corrects broken behavior |
| `docs` | Documentation only — no code change |
| `test` | Adds or corrects tests — no production code change |
| `refactor` | Restructures production code without changing behavior |
| `chore` | Maintenance — tooling, dependencies, config; no product or doc change |

Optional extras a project may adopt: `perf`, `build`, `ci`, `revert`. The `(scope)` is optional — the module or area touched.

## Branch / PR

- Branch + PR per ticket, always. Branch name `<ticket-id>-<slug>`.
- PR title: Conventional Commits style + ticket ID; PR description points to the return file.
- Review gate: orchestrator reviews the diff before merge → approve → CC merges; request changes → CC iterates.
- Parallel-safe tickets run on independent branches/PRs concurrently.

## Ticketing

Tracker-agnostic; the project picks its tracker at bootstrap.

- Ticket created at end of Scope (Backlog, ready to brief). Fast-lane trivial work gets no ticket — a one-line decisions-log row is the record.
- Estimate set at creation, refined at Brief, updated to actual at Close.
- **Closure comment** at Close: Shipped; Deferred (and where it went — new ticket ID or "future scope"); Spec/architecture drift; actual time; smoke result; follow-ups.
- Verify ticket IDs before posting anything to the tracker.
- Pre-existing tickets that drift get both their closure comment and their description corrected.
- Out-of-scope findings → new tickets.
- Recommended baseline labels: `bug`, `user-reported`, `needs-research`; projects add their own.

## Migrations

Idempotent (`IF NOT EXISTS` / `ON CONFLICT`), forward-only, applied via the project's documented procedure, verified with a sanity query. CC-applied.

## Quality gates

Lint + type-check + full test suite. All pass before CC hands work back.

## Infrastructure changes

Apply-then-PR is acceptable only for **additive / non-breaking** infra. Destructive changes (destroy, replace) are PR-first.

## Cost tracking (engineering / cloud projects)

For any project that deploys to the cloud or carries recurring external costs, cost tracking is wired in by default — surfaced explicitly at Scope as a default-on decision (opt-out recorded). Wired at bootstrap, Day 1: providers don't backfill billing exports, so late enablement permanently loses history. Includes: provider billing/cost export enabled, an in-project mechanism to surface current spend on demand, and an expected cost ceiling in the architecture doc.

## Estimation

- Orchestrator/operator set an estimate at ticket creation, refined at Brief — derived by querying `global/estimation-calibration.md` for the work-type + operator, not guessed fresh.
- CC returns the actual **work-time** in the Return Contract.
- At Close the orchestrator records: the actual work-time; **wait-time** (calendar/blocked time, kept separate so it never pollutes work-time); a one-line **variance reason**; the **work-type** tag.
- All appended to `global/estimation-calibration.md`, keyed by work-type + operator.

## Secrets hygiene

- Never paste or echo a secret in chat or screenshots.
- The operator populates secrets from their own terminal via file-based input (not `echo`, which lands in shell history).
- Confirm a secret via side-effect, never by printing the value.
- Leaked-secret response: stop the in-flight task, revoke at the provider, rotate, repopulate. Rotation cadence defined per project.
