# Handoff Protocol

All handoffs — between agents, and across sessions — are **file + pointer**: write a file, send a short pointer (the path, plus the ticket ID where relevant). Never paste full content into chat. Never use screenshots.

## Orchestrator → CC: the brief

- File: `orchestration/handoffs/<ticket-id>-<slug>-brief.md`
- The orchestrator writes it, mirrors its content into the tracker ticket, and hands the operator a short pointer prompt (ticket ID + path).
- Brief contents: see `engineering/sdlc.md` (Brief step).

## CC → orchestrator: the return file

- File: `orchestration/handoffs/<ticket-id>-<slug>-return.md`
- One file per ticket, progressively filled across checkpoints — see `engineering/return-contract.md`.
- CC writes it and hands the orchestrator a pointer.

## Naming

- `<ticket-id>` — the tracker ID (e.g. `PROJ-42`).
- `<slug>` — lowercase kebab-case, ~2–4 words from the ticket title.
- Session handoff — `session-handoff-<YYYY-MM-DDTHHMMZ>.md` (UTC, minute precision, filesystem-safe — no colons).

## Files & git

- Briefs and returns live in `orchestration/handoffs/` and are **gitignored** — transient (deleted at session end) and single-writer.
- **Rule:** a file may be gitignored only if it is single-writer. Anything with concurrent writers (decisions-log, failure-modes, learnings, drift-log) must be versioned — git is the concurrency control, and append-only discipline keeps merges trivial.
