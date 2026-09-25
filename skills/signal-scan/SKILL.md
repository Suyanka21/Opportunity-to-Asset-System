---
name: signal-scan
description: Scans a defined market, vertical, or timing window for fresh, evidence-backed signs of a small, time-sensitive problem someone would pay to have solved. Use at the start of any OAS opportunity hunt, whenever the founder gives a vertical/event/season brief or says something like "find me something" or "what's happening around X right now" — including seasonal-spending sweeps (e.g. back-to-school, holidays, tax deadlines). This skill only detects and logs candidate signals with evidence; it does not judge whether something is monetizable — hand every result to opportunity-scorer for that.
---

# Signal Scan

Covers the **observe → detect** stage of the OAS lifecycle. Read
`../../CONSTITUTION.md` and `../../GLOBAL_AGENT_INSTRUCTIONS.md` once per
session before running this — this file assumes both are already loaded and
does not repeat their content.

## Input

- Geography (default: Kenya, per Global Instructions §2)
- Vertical, theme, event, or season to scan (from the founder, or inferred
  from an explicit prompt like "next major seasonal spending period")
- Optional: a time window

If none of these are given, ask the founder for at least a vertical or
theme before scanning — an unscoped scan burns budget for no reason (Codex
principle).

## Procedure

1. **Check for existing coverage.** Before spending any research budget,
   check whether this scope/window already has a Signal Record still
   inside its freshness window (see `opportunity-ledger` for the log).
   If so, don't re-scan it — surface what's already there.
2. **Look for concrete friction, not vibes.** Prioritize things with a
   real artifact behind them: a deadline, a new rule taking effect, a
   price shock, a capacity shortage, a recurring complaint pattern, a
   seasonal spend spike. A vague sense that "people struggle with X" is
   not a signal until it has evidence behind it.
3. **Tag evidence honestly** using the taxonomy in Global Instructions §3
   as you go — don't write a Signal Record for something you only suspect
   without tagging it Hypothesis.
4. **Set a verify-by date** on each signal using the Freshness defaults
   table (Global Instructions §4), picking the row that matches the
   claim's volatility.
5. **Stop early.** This is a cheap detection pass — a handful of targeted
   look-ups, not exhaustive research (Cost principle). Stop once you have
   3–8 well-evidenced signals, or once you've exhausted a reasonable cheap
   budget for the scope given.
6. **Hand off, don't pre-judge.** List the Signal Records for the founder
   or for `opportunity-scorer`. Do not rank or recommend which to pursue —
   scoring buyer, price, and delivery feasibility is the next skill's job.

## Output

One Signal Record per candidate, using `templates/signal_record.md`.

## Stop / kill condition

If the scoped window genuinely produces nothing with real evidence within
the cheap budget, report that plainly — "no evidenced signal found in this
window" — rather than manufacturing a signal from hypothesis to look
productive.
