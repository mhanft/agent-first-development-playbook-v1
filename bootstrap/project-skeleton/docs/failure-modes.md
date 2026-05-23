# Failure Modes & Diagnostics — <PROJECT>

A symptom-first engineering reference. When something breaks, find the symptom, follow the diagnostic, apply the fix.

Each entry is marked **🔥 confirmed** (actually hit) or **⚠️ predicted** (plausible from the design, not yet seen), and follows: symptom → diagnostic steps → root cause → fix.

## Maintenance contract

- Any failure that took more than 30 minutes to diagnose gets an entry — record the verbatim symptom, the root cause, and the diagnostic sequence that found it.
- **Append-only — never renumber.** Append at the next free slot within a subsystem; existing numbers are stable references.
- ⚠️ predicted entries graduate to 🔥 confirmed the first time they're hit, with the date.
- Grep this file first when debugging.
- Cross-project lessons go to the methodology's `global/` learnings instead — this file is project-specific.

## Entries

_None yet._
