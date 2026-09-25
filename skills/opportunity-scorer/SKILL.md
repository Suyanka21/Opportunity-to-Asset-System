---
name: opportunity-scorer
description: Turns one Signal Record, or a founder-supplied problem, into a scored Opportunity Card — names the buyer, isolates the Minimal Monetizable Unit, checks 72-hour delivery feasibility, gives a defensible price range, and ends with a proceed/shrink/kill recommendation for the founder to decide on. Use whenever a signal needs validating, whenever the founder asks "is this worth pursuing" or "turn this into something I can sell in the next few days", and for re-scoring an existing Opportunity Card that opportunity-ledger flagged as due for re-verification. Never skip straight to a build recommendation without running this.
---

# Opportunity Scorer

Covers the **validate → isolate MMU → estimate commercial value → check
rapid-delivery** stage of the OAS lifecycle. Assumes `../../CONSTITUTION.md`
and `../../GLOBAL_AGENT_INSTRUCTIONS.md` are already loaded this session.

## Input

Either:
- A Signal Record from `signal-scan`, or
- A problem the founder states directly (skip straight to step 2), or
- An existing Opportunity Card being re-scored (see "Update mode" below)

## Procedure

1. **State the value, not the form.** One buyer-facing sentence describing
   the underlying value, with no technology or delivery form named yet
   (MMU discipline, Global Instructions §6).
2. **Name the buyer.** Who specifically has this problem, why now, and what
   evidence exists that they *can and would pay* — not just that the
   problem exists. No identifiable buyer with a willingness signal = kill
   here (Commercial principle). Tag every claim per the evidence taxonomy.
3. **Isolate the MMU.** The smallest single deliverable that lets that
   buyer act today. Actively reject SaaS/app/dashboard/automation as a
   default — a document, a curated list, a data point, a piece of
   outreach, or a decision can all be valid MMUs (Information principle).
4. **Check the 72-hour constraint.** Rough delivery estimate for the MMU as
   scoped. If it plausibly can't ship in ~72 hours, shrink it further, or
   explicitly park it as "not a first MMU — candidate for later" rather
   than forcing a fit.
5. **Price it honestly.** Give low / mid / high, each with its basis
   (comparable price, an actual willingness signal, cost-plus) and a
   confidence level. Never present one number as if it were precise when
   the underlying evidence is thin.
6. **Match research depth to the price tier** (Global Instructions §5) —
   don't spend deep-validation effort on a sub-$50 idea, and don't call an
   over-$500 idea validated without an actual buyer conversation.
7. **Recommend, don't decide.** proceed / shrink further / kill, plus the
   one or two cheapest things that would most raise confidence if the
   founder wants to proceed. Phrase this as advisory input — the founder
   makes the call (Human principle).
8. **Set a verify-by date** on the card (Global Instructions §4).
9. **Hand off for recording.** Pass the finished card to `opportunity-ledger`
   once the founder has made a decision on it, so the transaction dataset
   accumulates (Asset principle) — this skill does not maintain its own
   history.

## Update mode (re-scoring)

When given an existing Opportunity Card instead of a fresh signal (e.g.
because `opportunity-ledger`'s freshness sweep flagged it): re-run steps
2–6 against current evidence, then explicitly state, per dimension (buyer,
price, feasibility), whether it **strengthened, weakened, or is unchanged**
since the last card — don't just issue a new card with no comparison. This
is how portfolio reviews (see `opportunity-ledger`) get their "strengthened
/ weakened / stale" verdicts; opportunity-ledger itself only flags what
needs a look, it never re-scores.

## Output

One Opportunity Card using `templates/opportunity_card.md`.

## Stop / kill conditions

- No identifiable buyer with a willingness signal → kill, state why.
- MMU can't be shrunk to fit ~72 hours and there's no reason to park it for
  later → kill or explicitly downgrade to "future product idea, not an OAS
  MMU."
- Evidence for a claim central to the price or buyer case is Hypothesis
  only, and the price tier calls for corroboration → don't proceed to a
  price number yet; recommend the cheapest way to firm it up instead.
