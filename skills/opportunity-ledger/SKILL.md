---
name: opportunity-ledger
description: Records what actually happened to an Opportunity Card (pursued or declined, delivered on time, price achieved, outcome) and periodically reviews the accumulated log to flag stale opportunities needing re-verification and spot repeated patterns worth graduating into a reusable asset or product. Use after any founder decision on an opportunity, on a recurring portfolio-review cadence, or when asked to review previously identified opportunities and say which strengthened, weakened, went stale, or need another look. This is the only skill that reads or writes the historical OAS log — don't let signal-scan or opportunity-scorer keep their own separate history.
---

# Opportunity Ledger

Covers the **record evidence → identify repetition → graduate** stage of
the OAS lifecycle. Assumes `../../CONSTITUTION.md` and
`../../GLOBAL_AGENT_INSTRUCTIONS.md` are already loaded this session.

This skill has two modes. Recording is cheap and happens constantly;
review is a batch pass and should stay cheap too (Codex principle) — it
classifies, it does not re-research.

## Mode A — Record

Run this once per Opportunity Card, after the founder has made a decision
on it.

1. Append one Ledger Entry (`templates/ledger_entry.md`) referencing the
   card's `id`.
2. Always capture: the decision, who made it, whether it shipped within
   72h, actual price vs. the estimated range, and — even for a decline or a
   failure — one sentence of what this taught the system (Asset principle).
3. If an entry arrives without a clear human decision-maker attached, flag
   it: `⚠ decision-maker not confirmed as founder`. Don't silently assume
   the founder decided (Human principle).

## Mode B — Review (batch)

Run this when asked to review the portfolio, on a recurring cadence, or
before a new signal-scan pass to check for existing coverage.

1. **Freshness sweep.** Any open opportunity whose `verify-by` date has
   passed gets flagged `stale — re-verify or kill`, never silently carried
   forward as still valid. Route flagged cards to `opportunity-scorer`'s
   Update mode for the actual re-scoring — this skill classifies staleness,
   it does not re-score buyer/price/feasibility itself.
2. **Repetition sweep.** Group entries by (problem type × buyer type ×
   solution form). Working threshold (adjust freely — not in the
   Constitution): **3 or more paid instances** of essentially the same
   triple is enough to flag as a graduation candidate.
3. **Report, don't decide.** For each graduation candidate, summarize the
   repeated-demand evidence and let the founder decide whether to build the
   larger asset (Graduation + Human principles together). Never recommend
   graduation on the strength of interest, a pilot, or a single sale.
4. Anything neither stale nor a graduation candidate: no action needed —
   say so plainly rather than padding the review with filler.

## Output

- Mode A: one appended Ledger Entry.
- Mode B: a short Review Summary — stale list (routed to opportunity-scorer),
  graduation candidates with their evidence, and "nothing to report" where
  that's true.

## Stop / kill conditions

- Don't graduate on a single paid instance, however promising.
- Don't let a stale card sit un-flagged just because no one asked about it.
