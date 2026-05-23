# Engineering SDLC

The 7-step per-ticket cycle. Every non-trivial piece of engineering work runs through it. Trivial work takes the fast lane (Step 1).

Roles: `../common/roles.md`. Handoffs: `../common/handoff-protocol.md`. Decisions: `../common/decision-qa.md`.

## Step 1 — Scope

Turn a raw idea or bug into a fully-decided unit of work.

- Entry: operator raises a feature, change, or bug.
- Orchestrator inventories current state (docs, ticket state, code) before proposing anything.
- **Triage:** trivial → fast lane (skip to Code; commit + a one-line decisions-log row; no ticket, brief, or review). Otherwise → full Scope. *Trivial* = no schema change, no new/changed user-facing rule, small single-surface diff, no new dependency; orchestrator and operator both agree.
- Decision Q&A on every fork; research as needed.
- **Review gate (size/risk-gated):** for any architecture change, the senior-architect agent runs in Scope mode — reviews the whole application architecture, flags risks, suggests changes; its written review feeds the decision Q&A before anything locks.
- **Cost tracking:** for cloud or recurring-cost projects, the orchestrator surfaces cost-tracking as a default-on decision (opt-out recorded) — see `conventions.md`.
- Each locked decision recorded (one line in decisions-log, reasoning in decision-qa-log).
- Tracker ticket created (Backlog, ready to brief), with an initial estimate.
- Exit: every fork decided, ticket exists, work ready to brief.

## Step 2 — Brief

Turn a scoped ticket into an executable spec for CC.

- Orchestrator writes the brief to `orchestration/handoffs/<ticket-id>-<slug>-brief.md`, mirrors it into the ticket, hands the operator a short pointer prompt.
- Estimate refined here, informed by `global/estimation-calibration.md` for the work-type + operator.
- **Brief template** — required sections:
  1. Ticket ID + title
  2. Context — why this work, what triggered it
  3. Locked decisions — outcomes from Scope's Q&A
  4. Scope of work — what to build/change
  5. Files/modules expected to touch — best guess; non-binding, but drift from it must be reported
  6. Acceptance criteria
  7. Test + quality-gate expectations — test what a senior engineer would test; meaningful coverage of correctness-critical and regression-prone logic
  8. Out of scope / explicitly deferred
  9. Estimate
  10. Return requirements — the Return Contract fields CC must hand back, plus drift-reporting and closure reminders
- **Brief-writing convention:** every brief explicitly directs CC to parallelize its own execution where the work decomposes.
- **Parallelization pass:** once tickets are briefed, the orchestrator groups the ready set into parallel-safe batches — tickets whose files-to-touch don't overlap and that can run on independent branches. It proposes the batches; the operator runs them as separate concurrent CC sessions.
- Lifecycle: the brief file is kept through the session, deleted at wrap-up (closed tickets only).
- Exit: brief on disk + mirrored in ticket; pointer delivered.

## Step 3 — Code

CC builds the briefed work.

- CC reads the full brief file.
- **Inventory pass:** CC inventories the actual code first. If the brief contradicts the code, CC stops and surfaces the discrepancy (return file, "checkpoint 0") before writing anything — the orchestrator resolves it, updates the brief, hands the pointer back.
- CC implements the scope; parallelizes its own execution per the brief.
- CC writes tests — senior-engineer judgment.
- CC runs quality gates — lint + type-check + full test suite; all pass before handoff.
- **Self-review:** before opening the PR, CC spins three reviewers in parallel on the diff — independent code reviewer, security reviewer, architecture agent (Diff mode); see `review-agents.md`. CC addresses findings; findings + resolutions go verbatim into the return file.
- CC commits to a per-ticket branch; CC is the sole committer; Conventional Commits + ticket ID.
- CC opens a PR; the PR description = Return Contract checkpoint 1.
- Exit: PR open, checkpoint-1 return filled.

## Review gate (between Step 3 and Step 4)

The orchestrator reviews the diff against the brief + the checkpoint-1 return. Approve → CC merges. Request changes → CC iterates until clean.

## Step 4 — Deploy

Ship the merged change. CC-driven.

- CC runs the project deploy scripts (operator-run only against a recorded limitation).
- CC applies schema migrations — idempotent, forward-only, via the documented procedure.
- CC verifies the deploy (service healthy, live commit matches, migration sanity check).
- **Failure policy (hybrid):** a deploy failure → CC rolls back to known-good immediately. A bug surfaced later by smoke → orchestrator/operator decide rollback vs hotfix per severity.
- CC completes the return file — checkpoint 2 (deploy/migration status, final actual work-time).
- Exit: change live + verified; full Return Contract delivered.

## Step 5 — Smoke-test

Confirm the shipped change works live.

- Runs against the brief's acceptance criteria + CC's suggested smoke checklist (in the Return Contract).
- Agent-run where possible; operator-run where it needs real-world or human interaction.
- Diagnostics-first: on any failure, capture the symptom + logs before retrying. Anything >30 min to diagnose → a `failure-modes.md` entry.
- Loop: in-scope bugs iterate on the same ticket (Code → Deploy → Smoke again) until clean. Out-of-scope findings → new tickets.
- Exit: shipped change confirmed working live; outcome recorded on the ticket.

## Step 6 — Update docs

Reconcile documentation to what actually shipped — done last, because smoke often reveals behavior that drifted from the brief.

- **User-instructions** — updated if any user-facing change shipped (new/renamed/removed command, new error/message, changed user-hittable rule, changed UI). Schema-only, internal-refactor, and deploy-only changes don't trigger. Default to updating if unsure.
- **Architecture diagrams** — bumped if a structural change shipped (new table, event/command type, module, command, state-machine or IPC change).
- **Architecture drift** — the drift log is reconciled into the canonical architecture doc + diagrams.
- **failure-modes** — entries landed for any >30-min diagnoses from this cycle.
- These are in-repo docs → CC commits them.
- Exit: in-repo documentation matches shipped reality.

## Step 7 — Close

Orchestrator finalizes the ticket. Consumes the return file.

- Posts the closure comment (verify the ticket ID first): **Shipped**; **Deferred** (and where it went — new ticket ID or "future scope"); **Spec/architecture drift**; actual time; smoke result; follow-ups.
- Ticket → Done. Estimate field updated with the actual time.
- (estimate, actual) pair — work-type + operator tagged, work-time/wait-time split, variance reason — appended to `global/estimation-calibration.md`.
- Architecture drift appended to `orchestration/architecture-drift-log.md`.
- Decisions-log gets its one-line ship entry.
- Lessons confirmed landed (failure-modes; global learnings if generalizable).
- Out-of-scope findings → new tickets.
- Exit: ticket Done; records consistent across tracker, decisions-log, drift-log, estimation log, lessons.
