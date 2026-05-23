# Business Process

The lighter analog of the engineering SDLC, for business work — marketing, store operations, product decisions, supplier choices, and similar.

Reuses the full `../common/` layer: roles, decision Q&A, session lifecycle, lesson capture, handoff protocol.

Drops the engineering machinery: no CC-as-coder, no branch/PR/review-gate, no deploy/migrations, no code/security/architecture review agents.

## Roles

Operator + orchestrator. The orchestrator both scopes and executes the work (research, content, analysis, setup), spawning task subagents for parallelizable chunks. There is no standing implementing agent — there is no code repo.

## The cycle — 4 steps

### 1. Scope
Decide what to do and why, via decision Q&A. Decisions recorded (decisions-log + decision-qa-log). No senior-architect review.

### 2. Plan
Turn the decision into an action checklist — often just the decision + the steps. Estimate optional.

### 3. Execute
Orchestrator / operator / task subagents do the work; outputs land in the project folder. **Sign-off gate:** the operator approves before any irreversible or cost-incurring external action — publishing, sending a campaign, spending money. These can't be rolled back; this is the business analog of the engineering review gate.

### 4. Review & Close
Check the outcome, record results + lessons, close.

## Outcomes that mature over time

Business outcomes are often measured over days or weeks — a campaign, a price change, a new listing. Close can therefore be **provisional** ("executed; results pending"), with a **scheduled follow-up** to record the actual result against the expectation.

## Project structure

Business projects use the same `orchestration/` shape (decisions-log, session-handoffs) + a project folder for deliverables + a project lessons/retro file (the analog of `failure-modes.md`).

## Cost & revenue tracking

Not an auto-wired SOP — that is the engineering cloud-cost SOP. Every business plan designates **accounting/bookkeeping software** to track costs and revenue. It is operator-owned — real-world bookkeeping is not something an agent stands up on its own. Agents assist only when the operator has connected the relevant accounting tool/connector and explicitly asks (reconciliation, reporting, summaries).

## Tracker

Optional. Light initiatives live in the decisions log + handoffs; bigger multi-step initiatives can use a tracker.
