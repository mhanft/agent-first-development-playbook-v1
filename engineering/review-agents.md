# Review Agents

Transient specialist agents — spun up for a scoped review, gone when done. None is a standing role.

## The three diff-stage reviewers

On **every** code change, before opening the PR, CC spins three reviewers **in parallel** on the diff. Their findings + how CC addressed each go verbatim into the return file. CC addresses findings before opening the PR.

### Independent code reviewer

- Always runs a full review. Fresh context = independent — it did not write the code, so it isn't anchored on the author's assumptions.
- Covers correctness, edge cases, clarity, and whether the tests actually cover what they claim.

### Security reviewer

- **Self-gating.** First step: does the diff touch any security surface — auth, secrets, payments, PII, untrusted input? No → one-line "no security surface" verdict, stop. Yes → full security review.
- Self-gating (vs an orchestrator-applied gate) because security surfaces hide — the specialist is better placed than a generalist to spot a non-obvious one.

### Architecture agent — Diff mode

- **Self-gating.** Reads the diff against the brief's locked architecture decisions: did the code introduce or change architecture beyond what was decided? No → one-line verdict, stop. Yes → flag the drift and escalate to a full Scope-mode review.
- An independent drift detector — it does not rely solely on CC self-reporting drift.

## Architecture agent — Scope mode

Distinct from Diff mode. Runs at **Scope** (design time, before decisions lock), gated by any planned architecture change. Reviews the **whole application architecture**, not a diff — flags risks, suggests changes. Output is a written review in `orchestration/reviews/` that feeds the decision Q&A.

## No separate QA agent

Test authorship stays with CC — a senior engineer writes their own tests. Independent verification comes from the code reviewer + the orchestrator's PR review + operator smoke-testing.

## Orchestrator PR review

The orchestrator's own review at the review gate (between Code and Deploy) always happens — it is the backstop on top of CC's self-review.

## Subagents for big batches

Distinct from review. The orchestrator delegates large, mechanical batch operations (rule of thumb: >20 items, or anything that would flood the orchestrator's context) to a subagent — for context hygiene and reliability, not just speed. Brief the subagent with: ground-truth inputs, the pattern/rule with examples, an exclusion list of already-done items, an anti-duplication rule, and a punch-list report format for spot-checking.
