# Bootstrap Procedure

Run once per new project, before SDLC Step 1. Stands up a project that follows this methodology.

## 1. Scope the basics
Orchestrator + operator Q&A: project name; type (engineering / business / both); cloud-deployed?; single-repo or multi-repo (→ hub model); tracker choice. Record these as the first decisions-log entries.

## 2. GitHub auth
Operator confirms the `gh` CLI is authenticated on their machine (one-time; operator-owned — agents never handle credentials).

## 3. CC stamps the scaffold
CC creates the repo(s) with basic branch protection, the folder structure, all doc skeletons (from `project-skeleton/`), `.gitignore` (from `gitignore.template`), and a populated `CLAUDE.md` (from `CLAUDE.md.template`).

For a multi-repo project: a dedicated docs-only **hub repo** holds `CLAUDE.md` + `docs/` + `orchestration/`; each code repo carries a one-line pointer to the hub.

## 4. Tracker setup
Create the project in the chosen tracker; add the baseline labels (`bug`, `user-reported`, `needs-research`).

## 5. Cost tracking
If the project is cloud-deployed: enable the provider's billing/cost export Day 1, wire an in-project spend-surfacing mechanism, and run `cloud-day1-checklist.md`.

## 6. First commit + push
CC commits the scaffold and pushes.

## 7. Seed continuity
The orchestrator creates the first `session-handoff` file so future sessions have a save-point to read.

→ The project is now ready for SDLC Step 1 on its first real ticket.

## Folder layout stamped

```
<project-repo>/
  CLAUDE.md
  <application code>
  docs/
    architecture/            architecture doc + diagrams
    failure-modes.md
    user-instructions.md
  orchestration/
    decisions-log.md
    decision-qa-log.md
    architecture-drift-log.md
    reviews/                 senior-architect Scope-mode reviews
    session-logs/<user>/     session-handoff files (versioned)
    handoffs/                briefs + returns (gitignored)
```
