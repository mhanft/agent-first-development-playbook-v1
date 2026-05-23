# Decision Q&A

How decisions get made and recorded. Applies to all work — engineering and business.

## The pattern

At every fork, the orchestrator:

1. Presents 2–3 concrete options.
2. Recommends one, with reasoning.
3. Asks the operator to confirm or override.

The operator is the final authority. A decision is not settled until explicitly locked through this Q&A.

## Recording

Every locked decision is recorded twice:

- **`orchestration/decisions-log.md`** — one row per locked decision. The orchestrator log; ground truth for what is *not* up for re-debate.
- **`orchestration/decision-qa-log.md`** — the full dated Q&A reasoning behind each decision.

Both are appended at decision-lock time and at Close.

## Revisit triggers

A decision may be locked *with* a condition under which it is revisited — e.g. "revisit when revenue passes a threshold," "revisit at 6 months," "revisit if a competitor appears." Record the trigger on the decisions-log entry. A decision with a live trigger is still locked until the trigger fires.

## Superseding

Decisions are never deleted. When a decision changes, the new decision supersedes the old; both stay in the log with dates. The decision history is append-only.
