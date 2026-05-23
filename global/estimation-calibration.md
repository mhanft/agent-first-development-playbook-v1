# Estimation Calibration

Accumulated (estimate, actual) data so future estimates improve. Appended at every ticket Close (see `../engineering/conventions.md`). Append-only structured data — not deduped; if it ever grows unwieldy, summarize old rows into rolling aggregates.

## How to use it

At Brief, derive a ticket's estimate by querying this log for the matching **work-type + operator** — don't guess fresh.

## Schema

One row per closed ticket:

| Field | Meaning |
|---|---|
| date | Close date |
| ticket | Ticket ID |
| operator | Who directed the work |
| work-type | One of the work-type tags below |
| estimate | Estimated work-time |
| work-time | Actual hands-on agent/operator time |
| wait-time | Calendar/blocked time (deploy approval, third party, human cycle) — tracked, never folded into work-time |
| variance-reason | One line: why actual diverged from estimate |

## Work-type tags

Seed set, tunable as real data accumulates: `pure-code`, `ci-quality-gate-friction`, `fresh-cloud-setup`, `external-integration`, `calendar-bottlenecked`.

## Log

_No entries yet — populated at each ticket Close._

| date | ticket | operator | work-type | estimate | work-time | wait-time | variance-reason |
|---|---|---|---|---|---|---|---|
