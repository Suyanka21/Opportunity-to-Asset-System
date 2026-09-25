# OAS Skill Foundry

Portable Agent Skills for the Opportunity-to-Asset System (OAS), for use by
Claude Code, Google Antigravity, or OpenAI Codex.

## Load order (once per session, before any skill runs)

1. `CONSTITUTION.md` — the authoritative OAS Constitution. Skills reference
   it; they don't reproduce it.
2. `GLOBAL_AGENT_INSTRUCTIONS.md` — cross-cutting rules (authority model,
   geography default, evidence taxonomy, freshness defaults, research-depth
   discipline, MMU discipline) that every skill assumes but none repeats.

## Skills (lifecycle order)

| Skill | Lifecycle stage | Input | Output |
|---|---|---|---|
| `skills/signal-scan` | observe → detect | scope (geography/vertical/window) | Signal Records |
| `skills/opportunity-scorer` | validate → isolate MMU → estimate value → 72h check | a Signal Record or founder-stated problem (or a prior card, in Update mode) | Opportunity Card |
| `skills/opportunity-ledger` | record → identify repetition → graduate | founder decisions on cards; periodic review requests | Ledger Entries / Review Summary |

Typical flow: `signal-scan` → `opportunity-scorer` → founder decides →
`opportunity-ledger` (Mode A) records it. Run `opportunity-ledger` (Mode B)
periodically, or before a new `signal-scan` pass, to avoid re-covering
fresh ground and to catch graduation candidates.

## Design notes

- Three skills, not one per Constitution heading — see
  `SKILL_ARCHITECTURE_REPORT.md` for the decomposition reasoning.
- The shared reference files live at the repo root rather than being copied
  into each skill folder, because the target runtimes (Claude Code,
  Antigravity, Codex) read a project's files directly. If any skill here
  needs to be uploaded as a *standalone* Claude Skill (via claude.ai's Skill
  manager) independent of this repo, copy `CONSTITUTION.md` and
  `GLOBAL_AGENT_INSTRUCTIONS.md` into that skill's own `references/` folder
  first — a lone `.skill` upload won't see sibling files outside it.
- Numeric thresholds (freshness windows, research-depth price tiers, the
  3-paid-instance graduation bar) are working defaults, not constitutional
  mandates — the Constitution deliberately leaves these to judgment. Tune
  them in `GLOBAL_AGENT_INSTRUCTIONS.md` / `opportunity-ledger/SKILL.md`.
