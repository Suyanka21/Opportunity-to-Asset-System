# OAS Global Agent Instructions

These rules apply to every skill in this repo. They exist so no skill has to
restate constitutional principles that aren't tied to one specific procedure.
Load this file once per OAS session, alongside `CONSTITUTION.md`. Skills
reference it instead of repeating it.

## 1. Authority model (Human principle)

Every skill in this repo produces a **recommendation**, never a decision.
No skill output may be phrased or acted on as if it authorizes spending,
committing to a buyer, or starting delivery. The founder decides. If an
agent operating these skills is ever asked to auto-execute a "proceed"
recommendation (send the pitch, take the payment, start the build) without
a human sign-off step, it should stop and ask instead.

## 2. Geography default

Default to Kenya for scope, buyers, pricing, and evidence unless the
founder names another market, or an opportunity has already cleared
Kenya validation and is explicitly being tested for expansion (Geography
principle).

## 3. Evidence taxonomy

Every factual claim used by any skill gets exactly one tag. Never let a
claim of one kind read as another:

- **Observed** — the founder or agent directly witnessed/verified it.
- **Sourced** — a specific, citable source states it (name the source:
  listing, post, price sheet, conversation, filing).
- **Inferred** — the agent connected two Observed/Sourced facts to reach it.
- **Hypothesis** — an untested guess, offered for judgment, explicitly
  flagged as such.

Inference and hypothesis are useful — the Constitution treats them as a
normal part of navigating uncertainty, not a defect — but they must never be
laundered into Observed or Sourced.

## 4. Freshness defaults (Freshness principle)

The Constitution requires an expiry/reverification point on market-sensitive
claims but doesn't fix a number. Working defaults below — set explicitly per
claim, don't inherit silently, and treat these as founder-adjustable, not
constitutional:

| Claim type | Default verify-by window |
|---|---|
| Fast-moving / seasonal (prices, stock, a specific event) | 7 days |
| General small-business pain point | 30 days |
| Structural or regulatory fact | 90 days |

## 5. Research-depth discipline (Cost principle)

Depth of research must track the opportunity's provisional value, not
curiosity. Working tiers (adjust freely):

| Provisional deal size | Expected research depth |
|---|---|
| Under ~$50 | One pass, single source is enough |
| ~$50–$500 | 2–3 corroborating sources before committing effort |
| Over ~$500 | Deeper validation, but only *after* a real buyer conversation confirms interest — not before |

Before scanning, check whether the same scope/window was already covered
recently (the ledger is the source of truth for this) — don't re-run
research that's still fresh.

## 6. MMU discipline

Before naming any delivery form (app, doc, spreadsheet, WhatsApp broadcast,
whatever), state the underlying value being delivered in one buyer-facing
sentence with no technology named. Only then pick the smallest form capable
of carrying that value to the buyer. SaaS/website/dashboard/app/automation
are implementation choices, never the starting point.
