# Session Lifecycle

Session bookends layered on top of the per-ticket SDLC. They ensure any orchestrator can be swapped — crash, model change, fresh session — without losing context.

## Session start

The orchestrator reads its latest save-point first: `orchestration/session-logs/<user>/session-handoff-*.md` — the most recent by filename (ISO-UTC timestamps sort chronologically). Each project's `CLAUDE.md` hard-points at this.

## During the session

The orchestrator keeps a **live session log** current as it works — locked decisions, in-flight tickets, open threads, operator intent. This is crash insurance: if the orchestrator dies mid-session, a new one resumes from this file plus the canonical project docs.

## Session end — wrap-up

Triggered when the operator says "wrap up." Wrap-up activities:

1. Ensure the decisions log is current and the tracker reflects reality.
2. Ensure lessons from the session are captured.
3. Run the per-session light dedupe of the global learnings files (see `lesson-capture.md`).
4. Finalize the live session log into the save-point handoff.
5. Delete transient brief/return files for **closed** tickets only. In-flight tickets keep their files — they carry to next session, and the save-point points at them.

## The save-point file

`orchestration/session-logs/<user>/session-handoff-<YYYY-MM-DDTHHMMZ>.md` — UTC, minute precision, no colons (filesystem-safe). Created at session start, kept live through the session, finalized in place at wrap-up. Timestamped files are self-archiving; the next session reads the most recent.

Session-state files are **per-user** — continuity scratch for one orchestrator lineage, not project ground truth. They are never shared across users. (Project ground truth — decisions, failure-modes, learnings — stays shared and single; see `lesson-capture.md` and `handoff-protocol.md`.)
