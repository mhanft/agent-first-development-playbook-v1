# Team Expansion

This methodology is designed for a **single human operator** working with agents. This doc is a living, decision-by-decision assessment of which choices hold, need adjustment, or break as human team size grows.

It is a **parking lot** — actioned only if/when human teammates actually join. As the methodology evolves, new decisions get added as rows.

**Capture discipline:** when a decision is consciously a single-operator optimization, log it here as "current solo choice → what it becomes with human teammates."

Legend: ✅ scales as-is · ⚠️ needs adjustment · 🔴 won't work as-is / high-risk.

## SDLC cycle & gates

| Decision | 1 | 2–5 | 5+ |
|---|---|---|---|
| Fast lane — trivial work skips ticket/brief/review | ✅ | ⚠️ untracked changes invisible to others | 🔴 breaks audit trail — everything needs a ticket |
| Ticket created at end of Scope | ✅ | ✅ | ✅ |
| Senior-architect review on any architecture change | ✅ | ✅ | ✅ |
| Branch + PR per ticket | ✅ | ✅ | ✅ |
| Review gate = orchestrator reviews diff pre-merge | ✅ | ⚠️ add optional human review | ⚠️ required human reviewers + CODEOWNERS |
| CC self-spins 3 reviewers in parallel | ✅ | ✅ | ✅ |
| Parallelization — concurrent CC sessions on safe batches | ✅ | ⚠️ needs shared "who's touching what" | 🔴 needs a coordination layer |
| CC inventory pass before coding | ✅ | ✅ | ✅ |
| Deploy — CC-driven, hybrid failure policy | ✅ | ✅ | ⚠️ release coordination |
| Smoke-test — operator-run where human interaction needed | ✅ | ✅ | ✅ |
| Update-instructions as final step | ✅ | ✅ | ✅ |
| Architecture diagrams bumped at Step 6 | ✅ | ✅ | ✅ |

## Roles & authority

| Decision | 1 | 2–5 | 5+ |
|---|---|---|---|
| Three standing roles | ✅ | ⚠️ "operator" pluralizes | ⚠️ "operator" becomes a team with structure |
| Operator = single final decision authority | ✅ | 🔴 needs explicit owner/lead designation | 🔴 needs decision hierarchy by area |
| CC sole committer; orchestrator never commits source | ✅ | ✅ | ✅ |
| CC-driven by default | ✅ | ✅ | ✅ |
| Review-agent family | ✅ | ✅ | ✅ |
| No separate QA agent | ✅ | ✅ | ⚠️ dedicated QA may be warranted |

## Orchestrator continuity & sessions

| Decision | 1 | 2–5 | 5+ |
|---|---|---|---|
| Single orchestrator "brain" — concurrent decision-making on shared state | ✅ | 🔴 two brains editing shared project-state | 🔴 needs one coordinating orchestrator / strict ownership |
| Session-handoff — per-user namespaced | ✅ | ✅ | ✅ |
| Live session log — per-user | ✅ | ✅ | ✅ |
| Brief/return lifecycle (ticket-namespaced) | ✅ | ✅ | ✅ |
| Wrap-up dedupe of global files | ✅ | ✅ git merges disjoint appends | ⚠️ contention at scale |

## Handoffs & decision records

| Decision | 1 | 2–5 | 5+ |
|---|---|---|---|
| File + pointer handoffs both directions | ✅ | ✅ | ✅ |
| Return Contract (2-checkpoint file) | ✅ | ✅ | ✅ |
| Handoff model covers only agent↔agent / agent↔operator | ✅ | ⚠️ no human↔human channel | 🔴 needs comms + coordination system |
| Decisions double-logged (shared, versioned) | ✅ | ✅ git merges appends | ⚠️ contention grows |
| Architecture drift log (shared, versioned) | ✅ | ✅ | ⚠️ |
| failure-modes / learnings shared, append-only | ✅ | ✅ | ✅ |
| Orchestrator never describes architecture from memory | ✅ | ✅ | ✅ |
| Decision Q&A: 2–3 options, recommend, confirm | ✅ | ✅ | ✅ |

## Folder model, lessons & estimation

| Decision | 1 | 2–5 | 5+ |
|---|---|---|---|
| Single repo / orchestration hub | ✅ | ✅ | ✅ |
| Commit boundary (orchestrator docs / CC code+docs) | ✅ | ✅ | ✅ |
| 3-tier lesson capture | ✅ | ✅ | ✅ |
| failure-modes >30-min trigger | ✅ | ✅ | ✅ |
| Per-session light dedupe at wrap-up | ✅ | ✅ | ⚠️ |
| Heavyweight consolidation + promotion, owner-approved | ✅ | ⚠️ "owner" must be designated | ⚠️ |
| Estimation calibration keyed by work-type + operator | ✅ | ✅ already multi-person-ready | ✅ |

## Conventions, cost & business

| Decision | 1 | 2–5 | 5+ |
|---|---|---|---|
| Conventional Commits | ✅ | ✅ | ✅ |
| Closure-comment convention; verify ticket IDs | ✅ | ✅ | ✅ |
| Baseline labels | ✅ | ✅ | ✅ |
| Secrets hygiene | ✅ | ⚠️ per-person provisioning + rotation | ⚠️ least-privilege management |
| Subagents for big batches | ✅ | ✅ | ✅ |
| Cost-tracking SOP (engineering/cloud) | ✅ | ✅ | ✅ |
| Business cost = accounting software | ✅ | ✅ | ⚠️ dedicated bookkeeping role |
| Business process — 4-step light cycle | ✅ | ✅ | ✅ |
| Business roles (operator + orchestrator) | ✅ | ⚠️ pluralizes | ⚠️ |
| Business sign-off gate before irreversible actions | ✅ | ⚠️ who signs off — the owner | ⚠️ |

## Synthesis

Every remaining 🔴 is about **decision authority, concurrent decision-making, or human↔human coordination** — none is file plumbing. The engineering machinery scales as-is and gets more valuable with people. The multi-person problem reduces to one thing: **designate an owner and a coordination model.** Resolve those two and nearly every ⚠️ downstream resolves with them.
