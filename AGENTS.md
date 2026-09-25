# AGENTS.md — OAS Agent Operating Manual

This repository houses the **Opportunity-to-Asset System (OAS)**: an economic radar, offer generator, and rapid execution engine designed to discover, validate, and monetize time-sensitive needs in Kenya.

Every autonomous or paired agent (Claude Code, Google Antigravity, OpenAI Codex, etc.) entering this repository must strictly adhere to the following operational instructions.

---

## 1. Operating Sequence & Session Initialization

On every new session or task, load context in this exact order:
1. **[`constitution/OAS-CONSTITUTION.md`](constitution/OAS-CONSTITUTION.md)** (or root `CONSTITUTION.md`) — The supreme source of truth. Overrides all other files.
2. **[`GLOBAL_AGENT_INSTRUCTIONS.md`](GLOBAL_AGENT_INSTRUCTIONS.md)** — Cross-cutting operational rules (authority, geography, evidence tagging, freshness, research depth, MMU discipline).
3. **The target Skill specification** in `skills/<skill-name>/SKILL.md`.

Do not re-read or duplicate instructions that are already loaded.

---

## 2. Mandatory Rules of Engagement

1. **Human Decision Authority (Founder Principle)**: Agents advise, validate, and draft; the founder makes all commercial, commitment, and financial decisions. Never auto-commit or authorize execution without explicit human sign-off.
2. **Do Not Bypass Lifecycle Controls**: State moves sequentially:
   `signal-scan` → `opportunity-scorer` → Founder Decision → `opportunity-ledger`. Never skip validation to jump straight to building.
3. **No Fabricated Evidence or Market Data**: Every claim must be tagged (`Observed`, `Sourced`, `Inferred`, `Hypothesis`). Never launder guesses into sourced facts. If no evidence exists, state that plainly.
4. **Minimal Monetizable Unit (MMU) Discipline**: Name the value to the buyer in one plain sentence before proposing any delivery format. Do not build software, SaaS, or dashboards when a document, curated list, or direct intervention satisfies the need.
5. **The ~72-Hour Delivery Constraint**: Solutions must be deliverable within approximately 72 hours. If a concept cannot be shrunk to ~72 hours, park or kill it.
6. **No Silent Rule Changes**: Do not alter constitutional principles or promote provisional working defaults into rigid rules without founder mandate.
7. **Keep Outputs in the Repository**: Store Signal Records in `outputs/signals/`, Opportunity Cards in `opportunities/`, and Ledger summaries in `outputs/reviews/`. Maintain auditable state.
8. **Token & Context Efficiency (Codex Principle)**: Keep instructions lean, avoid speculative research, stop scans early once adequate signals are found, and check prior coverage in the ledger before spending budget.
9. **Working Defaults vs. Constitutional Law**:
   - *Constitutional Law*: Sole founder authority, Kenya-first, evidence taxonomy, ~72h MMU constraint, no product before repeated demand.
   - *Provisional Defaults (Founder-Adjustable)*: 7/30/90 day freshness windows, <$50/$50–$500/>$500 research tiers, and 3-paid-instance graduation threshold.

---

## 3. Skill Inventory

- **[`skills/signal-scan`](skills/signal-scan/SKILL.md)**: Detects concrete friction and produces tagged Signal Records. Does *not* evaluate monetizability.
- **[`skills/opportunity-scorer`](skills/opportunity-scorer/SKILL.md)**: Validates buyer, shrinks to MMU, checks 72h feasibility, models price range, and advises Proceed/Shrink/Kill. Handles Re-scoring (Update mode).
- **[`skills/opportunity-ledger`](skills/opportunity-ledger/SKILL.md)**: Logs decisions and learnings (Mode A); sweeps freshness and flags graduation candidates (Mode B). Sole home of historical data.

---

## 4. Current Repository Status

This is an **operating repository**, not a finished software product. Do not build web applications, APIs, databases, or frontend dashboards unless explicitly instructed for an approved, graduated MMU.
