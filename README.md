# Opportunity-to-Asset System (OAS)

A lean, agentic operating system designed to detect, validate, and rapidly monetize small, evidence-supported, time-sensitive economic needs in Kenya.

---

## 1. What OAS Is & Why It Exists

OAS is not a generic idea generator, an agency, or a software platform. It is an **economic radar + offer generator + rapid execution engine**.

Its purpose is to:
1. Scan for concrete economic friction and deadlines.
2. Shrink candidate solutions down to a **Minimal Monetizable Unit (MMU)** deliverable in **~72 hours**.
3. Formulate an honest value and pricing hypothesis for an identifiable buyer.
4. Provide structured advisory intelligence to the founder, who holds sole commercial authority.
5. Record every transaction outcome in an immutable ledger, systematically accumulating the critical dataset: *where people actually hand over money*.

---

## 2. Operating Hierarchy & Architecture

Implementation decisions follow this strict authority hierarchy:
1. **[`constitution/OAS-CONSTITUTION.md`](constitution/OAS-CONSTITUTION.md)** (or root `CONSTITUTION.md`) — Supreme operational law.
2. **[`GLOBAL_AGENT_INSTRUCTIONS.md`](GLOBAL_AGENT_INSTRUCTIONS.md)** — Cross-cutting rules (sole human authority, Kenya-first, evidence taxonomy, provisional freshness/research-depth defaults, MMU discipline).
3. **Skill Specifications** in `skills/` — The three lifecycle capabilities.
4. **Repository Organization & Implementation Details**.

---

## 3. The Three Canonical Skills

OAS strictly limits execution to three composable skills:

| Skill | Lifecycle Stage | Primary Input | Core Output |
|---|---|---|---|
| **[`skills/signal-scan`](skills/signal-scan/SKILL.md)** | Observe → Detect | Market/vertical scope & timing window | Tagged Signal Records |
| **[`skills/opportunity-scorer`](skills/opportunity-scorer/SKILL.md)** | Validate → Isolate MMU → Price → 72h Feasibility | Signal Record, founder prompt, or prior card | Opportunity Card |
| **[`skills/opportunity-ledger`](skills/opportunity-ledger/SKILL.md)** | Record → Review → Graduate | Founder decisions (Mode A) or cadence sweep (Mode B) | Ledger Entry / Review Summary |

### The Typical Lifecycle Loop
```text
[signal-scan] ──> Signal Record ──> [opportunity-scorer] ──> Opportunity Card
                                                                    │
                                                                    ▼
                                                            Founder Decision
                                                                    │
   ┌────────────────────────────────────────────────────────────────┴───────────────────┐
   ▼                                                                                    ▼
[Declined / Parked]                                                                 [Pursued]
   │                                                                                    │
   │                                                                                    ▼
   │                                                                            72-Hour Delivery
   │                                                                                    │
   └────────────────────────────────> [opportunity-ledger] <────────────────────────────┘
                                     (Mode A: Record Outcome)
                                                │
                                                ▼
                                    (Mode B: Periodic Sweeps)
                                     ├── Freshness: routes stale cards to scorer (Update mode)
                                     └── Repetition: flags 3+ paid instances for graduation
```

---

## 4. Repository Structure

```text
/
├── AGENTS.md                      # Operational guidelines for AI agents
├── README.md                      # High-level repository overview and execution model
├── GLOBAL_AGENT_INSTRUCTIONS.md   # Shared cross-cutting operational rules
├── CONSTITUTION.md                # Root mirror of the authoritative Constitution
├── constitution/
│   └── OAS-CONSTITUTION.md        # Authoritative OAS Constitution
├── skills/
│   ├── signal-scan/               # Detection skill
│   ├── opportunity-scorer/        # Validation, MMU shrinking & pricing skill
│   └── opportunity-ledger/        # Audit, repetition & graduation tracking skill
├── templates/
│   ├── signal_record.md           # Schema for detected signals
│   ├── opportunity_card.md        # Schema for scored opportunities
│   └── ledger_entry.md            # Schema for transaction outcomes
├── opportunities/                 # Storage for generated Opportunity Cards (OPP-*)
├── outputs/                       # Audit logs, scan outputs, and review summaries
└── docs/
    ├── OAS CONSTITUTION.md        # Reference constitution copy
    ├── TODO.md                    # Integration & repository architecture mandate
    └── REPOSITORY_ARCHITECTURE.md # Architectural report and dry-run audit
```

---

## 5. What This Repository Is NOT Yet

This is the canonical **operating system and architecture repository**. It is **NOT**:
- A consumer-facing web application or dashboard.
- A database or SaaS backend.
- A collection of speculative market research scripts.

Product building only occurs after repeated, verified paid demand is logged in the ledger.
