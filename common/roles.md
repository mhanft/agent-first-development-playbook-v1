# Roles

Three standing roles, plus transient specialist agents. The methodology assumes one human.

## Operator (human — the owner)

- Sets priorities; picks what to work on.
- Participates in decision Q&A; **final authority on every fork.**
- Runs the implementing-agent (CC) sessions; hands CC the pointer prompts.
- Runs smoke-tests that need real-world or human interaction; decides rollback vs hotfix for smoke-surfaced bugs.
- Triggers session wrap-up.
- Owns credentials and one-time auth setup.
- Does not write code or run scripts unless they choose to, or CC is genuinely blocked.

## Orchestrator (Claude — the planning + coordination brain)

- Owns scoping, decision Q&A, briefs, ticketing, orchestrator-side docs, PR review, architecture-drift reconciliation, estimation logging, session handoff.
- Inventories current state before proposing anything.
- Proposes parallel-safe ticket batches; spins up specialist agents and subagents.
- Commits orchestration docs. **Never touches or commits source code.**

## Implementing agent (CC — Claude Code)

- Does all coding, testing, committing, deploying, migrations — CC-driven by default.
- Reads briefs from files; writes return files; opens one PR per ticket; iterates on review feedback.
- Reports drift + actuals via the Return Contract; maintains in-repo docs (failure-modes, user-instructions, architecture diagrams).
- Parallelizes its own work where the brief directs. May run as multiple concurrent sessions across parallel-safe tickets.

## Transient specialist agents

Spun up for a scoped task, then gone. Full detail in `engineering/review-agents.md`.

- **Senior-architect agent** — reviews architecture. Scope mode: whole-system, gated by any architecture change. Diff mode: per-diff drift check.
- **Security reviewer** — reviews any code diff for security surface; self-gating.
- **Independent code reviewer** — reviews every code diff.

## Hard boundaries

- Orchestrator never commits source; CC is sole committer of code + engineering docs; orchestrator commits orchestration docs.
- Operator doesn't code or run scripts unless by choice, or CC is blocked (limitation recorded).
- Handoffs are always file + pointer.
- Decisions locked by orchestrator + operator (operator final); CC executes and reports drift, never silently re-decides.
