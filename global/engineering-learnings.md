# Engineering Learnings

Cross-project engineering lessons — generalized principles, transferable to any future project. Tier 2 of lesson capture (see `../common/lesson-capture.md`).

Format: index first, full entries below. Each entry: the lesson → context → what to do differently. Append-only during sessions; deduped at wrap-up; strong recurring lessons get promoted into the methodology and retired from here.

_Seeded from prior projects; grows via the lesson-capture process._

## Index

1. Start the failure-modes file in week one.
2. Verify public-API capability empirically before architecting on it.
3. When users report missing data, check timing windows before assuming a code bug.
4. Brief against the artifact (the code), not the intent (the architecture doc).
5. Spec drift caught before coding is the system working.
6. Any "multiplier" / "rate" / "odds" spec needs a worked example.
7. Never swallow errors with a bare except.
8. Cross-reference ground truth before mapping ambiguously-named third-party fields.
9. Ship diagnostic capture before retry heuristics.
10. Never delegate understanding.
11. Confirm a platform's portal state before flipping a dependent code flag.
12. Get a known-good reference before guessing at undocumented formats.

## Entries

### 1. Start the failure-modes file in week one
Create `docs/failure-modes.md` at project bootstrap, empty. The value compounds — an empty file in week one beats the file you wish you'd started once you're debugging in month three.

### 2. Verify public-API capability empirically before architecting on it
An architecture was built on a documented Web API field that turned out never to be populated for the relevant case — falsified only by a direct test. Public APIs sometimes have capability gaps that competitors bypass via private channels. Probe the actual endpoint with real data before committing an architecture to it.

### 3. When users report missing data, check timing windows before assuming a code bug
A reported "missing payout" was correct data shown during an in-flight settlement window. Before debugging code, check whether an in-progress process explains the observation.

### 4. Brief against the artifact, not the intent
The architecture doc describes intent; the code is the artifact. A brief written only against docs drifts from reality. CC does an inventory pass on the actual code before coding and stops if the brief contradicts it.

### 5. Spec drift caught before coding is the system working
When an agent flags that the spec and the code disagree, don't override with "just do X" — investigate which is wrong, fix the spec or the code, then proceed.

### 6. Any "multiplier" / "rate" / "odds" spec needs a worked example
"payout = stake × multiplier" was implemented literally; the intent was winnings on top of the returned stake. A worked example ("500 at 1.2× pays 1,100 = 500 refund + 600 winnings") removes the ambiguity.

### 7. Never swallow errors with a bare except
A broad `except` swallowed a TypeError; a refresh silently failed for a full deploy. Silent failures cost 2–3× the debug time of loud ones. Log the trace; never catch-and-drop.

### 8. Cross-reference ground truth before mapping ambiguously-named third-party fields
A third-party schema had two plausibly-named fields for "the same" value; the wrong one was mapped and a UI value froze for two days. When a schema has multiple candidates, verify against an independent ground truth before mapping.

### 9. Ship diagnostic capture before retry heuristics
Adding blanket retries on top of poor diagnostics masks distinct failure modes. Capture full error detail first; the diagnostics often reveal that "one bug" is several.

### 10. Never delegate understanding
An agent should know what every line of code and config does, not paste from training data. Applies to the orchestrator and the implementing agent alike.

### 11. Confirm a platform's portal state before flipping a dependent code flag
A privileged platform feature must be enabled both in the provider's portal and in code; flipping the code flag alone crashes at startup. Confirm the portal state first.

### 12. Get a known-good reference before guessing at undocumented formats
Three rounds of guessing an undocumented URL format cost ~40 min; the operator's working reference resolved it in 15. For any undocumented external format, get a known-good example before constructing your own.
