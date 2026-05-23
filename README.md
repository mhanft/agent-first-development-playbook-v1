# Agent-First Development Playbook

**What this is:** a complete operating methodology for **agent-first software development and business-building, run by a single human operator.** The agents do the execution — an orchestrator plans and coordinates, an implementing coding agent (Claude Code / "CC") writes, tests, and ships all code, and transient specialist agents review it. The human operator **directs**: sets priorities, owns every decision, holds final authority. Every project runs as a unit of one human + their agents.

**Scope assumption — read this first:** the entire methodology (SDLC, roles, decision authority, file conventions, session model) assumes that single operator. It is **not designed for multi-person human teams as-is.** Adding people changes parts of the SOP — see [`common/team-expansion.md`](common/team-expansion.md) for a decision-by-decision assessment of what holds, what needs adjustment, and what breaks at 2–5 and 5+.

## If you're an agent landing here

You're working on a project that points at this methodology. Identify your role below, follow its read-order, and operate by it. This repo is your operating manual — don't skip it.

## Session-start read-order, by role

**Orchestrator** — your latest `orchestration/session-logs/<you>/session-handoff-*.md` → the project's `orchestration/decisions-log.md` → `docs/failure-modes.md` → the architecture doc → methodology docs (`common/`, `engineering/`) as needed.

**Implementing agent (CC)** — the brief file you were pointed at → inventory the project code it references → `engineering/sdlc.md` (Code step) + `engineering/return-contract.md` for your operating model → `docs/failure-modes.md` before debugging.

**Review agent / subagent** — your spawn brief is self-contained. Read only what it points you to.

## Roles

- **Orchestrator** — the planning + coordination brain. Scopes work, runs decision Q&A, writes briefs, reviews CC's output, maintains records. Never touches source code. → `common/roles.md`, `engineering/sdlc.md`
- **Implementing agent (CC)** — does all coding, testing, committing, deploying. → `engineering/sdlc.md`, `engineering/return-contract.md`
- **Transient specialist agents** — code / security / architecture reviewers. → `engineering/review-agents.md`

The single human is the **operator** (the owner): sets priorities, final authority on every decision.

## The non-negotiables

1. The orchestrator never commits or edits source code. CC is the sole committer of code.
2. Handoffs are always **file + pointer** — write a file, send a path. Never paste full content or screenshots.
3. Decisions are locked by orchestrator + operator together (operator final). CC executes them and reports any drift — it never silently re-decides.
4. CC-driven by default — agents do all code, scripts, deploys, migrations. The operator does so only by choice, or when CC is genuinely blocked (and the limitation is recorded).
5. Never describe a project's architecture from memory — read the canonical architecture doc + drift log + the repo.
6. Never paste or echo a secret.
7. Anything that costs more than 30 minutes to diagnose becomes a `docs/failure-modes.md` entry.

## Repo map

- `common/` — practices shared by all work: roles, decision Q&A, session lifecycle, lesson capture, handoff protocol, team-expansion.
- `engineering/` — the engineering SDLC: the 7-step cycle, review agents, conventions, the return contract.
- `business/` — the lighter business process.
- `global/` — cross-project accumulated knowledge: engineering + business learnings, estimation calibration, reusable playbooks.
- `bootstrap/` — the kit for standing up a new project.
