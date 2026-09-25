# OAS Skill Architecture Report

## 1. Skills created

- `signal-scan`
- `opportunity-scorer`
- `opportunity-ledger`

Three skills, not nine. The Constitution has far more headings than that,
but most of them (Purpose, Primary objective, Research/Market/Commercial
principles, Geography, Freshness, Human, Asset, Codex, Cost principles) are
either top-level orientation or cross-cutting parameters — not independent
procedures. Only three genuinely distinct *activities* exist in the
lifecycle, grouped by what they produce:

| Activity | Constitution headings it absorbs | Skill |
|---|---|---|
| Find & log candidate friction | observe, detect | `signal-scan` |
| Validate, price, and time-check one candidate | validate, isolate the MMU, estimate commercial value, determine rapid delivery | `opportunity-scorer` |
| Track what happened & spot patterns | record evidence, identify repetition, graduate | `opportunity-ledger` |

## 2. Purpose of each skill

- **signal-scan** — cheap, evidence-tagged detection of time-sensitive
  friction in a scoped market. Produces raw material; makes no
  monetizability judgment.
- **opportunity-scorer** — the commercial reasoning core. Names a buyer,
  shrinks the idea to an MMU, checks the 72h constraint, prices it with an
  honest range, and issues an advisory proceed/shrink/kill call. Also
  handles re-scoring (Update mode) so portfolio reviews aren't a fourth
  skill.
- **opportunity-ledger** — the only place OAS history lives. Records
  outcomes one at a time, and on a batch pass flags staleness and detects
  repeated (problem × buyer × solution) patterns worth graduating.

## 3. Trigger for each skill

- `signal-scan`: a vertical/event/season brief, "find me something",
  seasonal-spending sweeps.
- `opportunity-scorer`: "is this worth pursuing", "turn this into something
  sellable in a few days", any Signal Record needing validation, or a card
  flagged stale by the ledger (Update mode).
- `opportunity-ledger`: after any founder decision on a card (Mode A);
  portfolio-review requests, or a pre-scan coverage check (Mode B).

## 4. Inputs and outputs

See `README.md`'s lifecycle table — kept in one place to avoid duplicating
it here.

## 5. Supporting files created

- `templates/signal_record.md`, `templates/opportunity_card.md`,
  `templates/ledger_entry.md` — one per skill, each earning its place
  because the three skills hand structured data to each other and need a
  stable shape to do it. No `scripts/` or `assets/` were created: nothing
  here is deterministic/repetitive enough to warrant executable code yet,
  and there's no visual/branding asset to bundle.
- `GLOBAL_AGENT_INSTRUCTIONS.md` (repo root, not a skill) — see §7.

## 6. Overlap removed

- Collapsed four validate-stage Constitution headings into one
  `opportunity-scorer` skill instead of four, since they share one
  procedure and one output artifact (the Opportunity Card).
- Collapsed record/repetition/graduation into one `opportunity-ledger`
  skill instead of three, since they share one data store (the log) and
  splitting them would have meant two skills both needing read/write access
  to the same history.
- Re-scoring an existing card (needed for portfolio reviews) was *not* made
  a fourth skill — it's an explicit mode of `opportunity-scorer`, since the
  procedure (re-check buyer/price/feasibility) is identical to first-time
  scoring; only the framing (state what changed) differs.

## 7. Constitutional instructions intentionally kept outside skills

Held in `GLOBAL_AGENT_INSTRUCTIONS.md` (loaded once, referenced by all
three skills) rather than repeated per-skill:

- Human principle → authority model (§1)
- Geography principle → default market (§2)
- A shared evidence taxonomy (Observed/Sourced/Inferred/Hypothesis), used
  by all three skills, defined once (§3)
- Freshness principle → concrete verify-by windows (§4)
- Cost principle → research-depth-by-value tiers (§5)
- MMU discipline as a general habit, not just inside the scorer (§6)

Purpose, Primary objective, Research/Market/Commercial principles (in their
general form), and the closing "economic radar" framing stay in
`CONSTITUTION.md` only — they're orientation for whoever operates this
system, not instructions a skill executes.

## 8. Unresolved ambiguity requiring founder review

- **Numeric thresholds are invented, not constitutional.** The freshness
  windows (7/30/90 days), the research-depth price tiers (<$50, $50–$500,
  >$500), and the graduation bar (3 paid instances) are defensible working
  defaults the Constitution deliberately left to judgment — not rules
  derived from it. Njoroge should tune or override them.
- **Packaging assumption.** These are built as a repo meant to be read
  directly by a coding agent (Claude Code / Antigravity / Codex), with
  shared reference files at the root. If any single skill needs to be
  uploaded standalone to a Skill manager that only bundles one folder, its
  shared references need to be copied in first (noted in `README.md`).
- **Where the ledger physically lives** (flat markdown file vs. a
  spreadsheet vs. a small database) is left to whichever runtime operates
  the system — the template is plain markdown so any of the three agents
  can append to it without extra tooling, but this wasn't specified and
  could be revisited once real volume shows up.

## 9. Recommended execution order

1. `signal-scan` (skip if the founder already hands you a problem)
2. `opportunity-scorer` on each surviving signal
3. Founder decision (outside any skill)
4. `opportunity-ledger` Mode A (record the decision/outcome)
5. `opportunity-ledger` Mode B, periodically or before the next `signal-scan`
   pass (freshness + repetition sweep; routes stale cards back to step 2 in
   Update mode)

---

## Dry-run against the three missions

No research was performed for these — they're a structural check that the
three skills compose correctly, per the mission's own instruction not to
run enormous research for the test.

**Mission A — seasonal spending period, Kenyan businesses.**
`signal-scan` (scope: Kenya, vertical: general SMB, window: the upcoming
season) surfaces evidence-tagged signals — e.g. a spending deadline or
capacity crunch tied to the season. `opportunity-scorer` takes the
strongest one, names the buyer (e.g. parents, or the SMBs serving them),
isolates a non-app MMU (a comparison list, a short guide, a curated
broadcast — not a dashboard), checks it ships in ~72h, and prices it with a
range. Composes cleanly; no gap.

**Mission B — small-business problem → paid 72h digital intervention.**
Enters directly at `opportunity-scorer` with a founder-supplied problem
(skipping `signal-scan`, which the skill explicitly supports). Same MMU /
72h / price procedure applies. No gap.

**Mission C — review prior opportunities for strengthened / weakened /
stale / needs-investigation.**
This is `opportunity-ledger` Mode B's freshness sweep, but "strengthened or
weakened" needs an actual re-evaluation, not just a stale/fresh label —
that's why `opportunity-scorer`'s Update mode exists: the ledger flags
what's due for a look, the scorer re-runs the buyer/price/feasibility check
and reports the delta. Without Update mode this mission would have needed
a fourth skill or forced the ledger to duplicate scoring logic; with it,
the existing two skills cover the mission together. No gap; no skill was
unnecessary and none was missing.

**READY FOR ANTIGRAVITY INTEGRATION**
