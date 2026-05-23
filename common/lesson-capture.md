# Lesson Capture

Capture anything that would cost again if forgotten. Three tiers, escalating as far as the lesson is worth.

## Tier 1 — Project-specific → `docs/failure-modes.md`

The concrete incident: symptom → diagnostic steps → root cause → fix. Marked **🔥 confirmed** (actually hit) or **⚠️ predicted** (plausible from the design, not yet seen).

- Trigger: any bug or failure that took more than 30 minutes to diagnose.
- **Append-only — never renumber.** Append at the next free slot within a subsystem; existing entry numbers are stable references. This rule also keeps concurrent appends merge-clean.
- Owner: CC (in-repo doc). Created empty at project bootstrap — start it before there's anything to put in it; the value compounds.

## Tier 2 — Global / cross-project → `global/engineering-learnings.md` or `global/business-learnings.md`

The *generalized* principle — what to do differently on a future, different project.

- Trigger: "would this help on a different project?"
- Entry shape: the lesson (one line) → context / originating incident (dated, with project anchor) → what to do differently. Note the cost incurred where known.
- Owner: orchestrator; promoted at Close or session wrap-up; cross-referenced to the originating failure-modes entry.
- Many lessons land in both tiers — concrete in failure-modes, generalized in global.

## Tier 3 — Methodology-level → the methodology docs themselves

If a lesson is strong or recurring enough to be a standing rule, it is promoted into the methodology (a line in conventions / SDLC / etc.) and **retired from the learnings file**. Promotion requires the methodology repo owner's approval.

## File structure

Global learnings files are **index + entries**: a one-line-per-lesson index on top, full entries below, grouped by category. Agents read the index by default, drill into an entry on demand.

## Consolidation

- **Per session (light):** at wrap-up, reconcile only *this session's* new lessons — check each against the existing set, merge or place. Bounded cost, independent of file size.
- **Heavyweight pass (rare):** accumulation-triggered (~15 new lessons since the last pass; tunable) or on demand. Scans the global files + sweeps every project's `failure-modes.md`. Produces: a dedupe/prune, promotion candidates (each with proposed methodology wording + slot), and missed generalizations (concerns logged in multiple projects but never globalized). Promotions are owner-approved.

The learnings files have an **exit** — strong lessons get promoted out (tier 3), stale ones retired. They are a waystation, not a landfill.
