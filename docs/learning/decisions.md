# Decisions

The live rulebook: everything that binds work in flight, which is why this file
is @-imported. master.md is orientation — read at phase boundaries, not here.

## Standing constraints (C-xx)
Rules that bind choices not yet made. Test: would violating this in a future
phase be a bug, or merely a different design? Only a bug belongs here. A decision
is promoted to a constraint when a SECOND phase has to honour it.

- **C-01 <constraint, stated so that it can be violated>**
  - Why: <mechanism, not preference>

## Standing checks (re-run per change, never "closed")
A constraint is a rule to honour; a standing check is a question to re-ask.
Record the trigger, not the current answer.
- **<check>** — trigger: <what makes this need re-running>

## Pre-harness decisions (imported from archive)
From phases that predate this harness, extracted only where still load-bearing.
Each entry names the archive file it came from. "Verified by" is "not yet" unless
re-proved under this harness — the original docs had no code access and cannot
count as evidence.


## Phase <N> decisions
<!-- ID format: D<phase>-<nn>, no spaces, e.g. D7-01. Constraints are C-01, C-02.
     /recall and /reflect locate entries by these IDs, so they must be greppable
     and must never be renumbered once written. -->
- **D<N>-01** <decision>
  - Why: <mechanism, not preference>
  - Rejected: <alternative>, because <reason>
  - Revisit if: <condition that would reopen it>
  - Verified by: <test / HTTP probe / DB state / console behavior / not yet>