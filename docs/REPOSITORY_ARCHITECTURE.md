# OAS Repository Architecture & Integration Report

This document defines the canonical architecture of the Opportunity-to-Asset System (OAS) repository, established by the Repository Architect and Integration Agent per [`docs/TODO.md`](TODO.md).

---

## A. Final Repository Structure

```text
Opportunity-to-Asset-System/
├── AGENTS.md                      # Operational handbook for all AI coding agents
├── README.md                      # Root architectural overview and execution loop
├── GLOBAL_AGENT_INSTRUCTIONS.md   # Shared cross-cutting operational rules
├── CONSTITUTION.md                # Root mirror of the authoritative OAS Constitution
│
├── constitution/
│   └── OAS-CONSTITUTION.md        # Authoritative OAS Constitution (Source of Truth)
│
├── skills/
│   ├── signal-scan/
│   │   ├── SKILL.md               # Detection skill definition
│   │   └── templates/
│   │       └── signal_record.md   # Local fallback template for standalone export
│   ├── opportunity-scorer/
│   │   ├── SKILL.md               # Scoring, shrinking & pricing skill definition
│   │   └── templates/
│   │       └── opportunity_card.md# Local fallback template for standalone export
│   └── opportunity-ledger/
│       ├── SKILL.md               # History, staleness & repetition tracking skill
│       └── templates/
│           └── ledger_entry.md    # Local fallback template for standalone export
│
├── templates/                     # Centralized canonical schemas
│   ├── signal_record.md           # Schema for candidate signals
│   ├── opportunity_card.md        # Schema for scored opportunities (MMU)
│   └── ledger_entry.md            # Schema for transaction outcomes & learnings
│
├── opportunities/                 # Persistent opportunity records
│   └── README.md                  # Lifecycle, naming conventions (OPP-*), and guidelines
│
├── outputs/                       # Auditable run artifacts and operational summaries
│   └── README.md                  # Conventions for signals, reviews, and graduations
│
└── docs/                          # Authoritative documentation and architecture reports
    ├── OAS CONSTITUTION.md        # User-supplied reference copy of the Constitution
    ├── TODO.md                    # Integration & repository architecture mandate
    └── REPOSITORY_ARCHITECTURE.md # This document
```

---

## B. Authority Hierarchy

All implementation and operational reasoning must respect this exact four-tier hierarchy:

1. **OAS Constitution** ([`constitution/OAS-CONSTITUTION.md`](../constitution/OAS-CONSTITUTION.md) / [`CONSTITUTION.md`](../CONSTITUTION.md)):
   The supreme governing document. Defines core principles: sole founder authority, Kenya-first default, evidence before assumption, Minimal Monetizable Unit (MMU) core unit, ~72-hour delivery discipline, cost-proportional research, and anti-premature productization.
2. **Claude-Created 3-Skill Architecture**:
   The core lifecycle decomposition into `signal-scan`, `opportunity-scorer`, and `opportunity-ledger`. New skills may not be arbitrarily added; concepts belong in global instructions, skill modes, or templates.
3. **Skill Specifications & Templates**:
   Definitions in `skills/*/SKILL.md` and schemas in `templates/`.
4. **Repository Organization & Implementation Details**:
   Directory layouts, logging conventions, and file path arrangements.

---

## C. Skill Map

| Field | Skill 1: `signal-scan` | Skill 2: `opportunity-scorer` | Skill 3: `opportunity-ledger` |
|---|---|---|---|
| **Lifecycle Role** | Observe → Detect | Validate → Isolate MMU → Price → 72h Feasibility | Record → Review → Graduate |
| **Purpose** | Cheap, evidence-tagged detection of real-world friction and deadlines. Does not judge monetizability. | Isolates the MMU, identifies the buyer, establishes price ranges, tests 72h delivery, and advises on next steps. | Single historical source of truth. Logs transactions (Mode A) and conducts batch portfolio reviews (Mode B). |
| **Trigger** | Vertical/season brief, "find me something", or regular scan cadence. | Fresh Signal Record, direct founder-stated problem, or stale card flagged by ledger. | Founder decision on a card (Mode A); portfolio review or pre-scan coverage check (Mode B). |
| **Inputs** | Scope (geography: Kenya default, vertical, theme, window). | Signal Record, direct problem statement, or existing card (Update Mode). | Mode A: Scored card + founder decision.<br>Mode B: Portfolio of logged entries. |
| **Outputs** | Tagged Signal Records (`templates/signal_record.md`). | Scored Opportunity Card (`templates/opportunity_card.md`). | Mode A: Appended Ledger Entry.<br>Mode B: Portfolio Review Summary. |
| **Stop Conditions** | Cheap budget reached or no evidenced friction found (no manufactured signals). | No buyer with willingness signal, or solution cannot shrink to ~72h. | Never graduate on single instance; never carry stale claims forward silently. |

---

## D. State Flow

State moves unidirectionally with clear human approval gates:

```text
[ Real-World Friction ]
          │
          ▼
   1. signal-scan
   (Outputs: Signal Record with evidence tags & verify-by dates)
          │
          ├────────────────────────────────────────┐
          ▼                                        ▼
   2. opportunity-scorer                   Direct Founder Prompt
   (Names buyer, isolates MMU, prices,     (Enters scorer directly,
    checks 72h delivery, recommends)        skipping signal-scan)
          │
          ▼
   [ Opportunity Card ]
          │
          ▼
   3. Founder Decision Gate (Advisory → Human Approval)
          │
     ┌────┴──────────────────────────┐
     ▼                               ▼
 [Declined / Parked]             [Pursued]
     │                               │
     │                         72-Hour Rapid Delivery
     │                               │
     └───────────────┬───────────────┘
                     ▼
   4. opportunity-ledger (Mode A: Record Outcome)
   (Captures: buyer outcome, actual price vs estimate, delivery time, system learnings)
                     │
                     ▼
   5. opportunity-ledger (Mode B: Batch Periodic Review)
     ├── Freshness Sweep ───> [Stale Cards] ──> Routes to opportunity-scorer (Update Mode)
     └── Repetition Sweep ──> [≥3 Paid Instances] ──> Graduation Proposal Dossier
```

---

## E. Global Agent Instructions Rationale

[`GLOBAL_AGENT_INSTRUCTIONS.md`](../GLOBAL_AGENT_INSTRUCTIONS.md) contains cross-cutting operational rules that apply across all agent sessions and skills:

1. **Authority Model**: Re-affirms that skills produce advice, not binding decisions. Protects founder decision-making and prevents runaway execution.
2. **Geography Default**: Defaults all scopes and buyer assumptions to Kenya unless explicitly told otherwise.
3. **Shared Evidence Taxonomy**: Standardizes all claims across all skills into `Observed`, `Sourced`, `Inferred`, or `Hypothesis`.
4. **Provisional Freshness Defaults**: Establishes working verify-by windows (7/30/90 days) based on claim volatility.
5. **Research-Depth Discipline**: Enforces budget proportionality (<$50, $50–$500, >$500) to keep research lean.
6. **MMU Discipline**: Mandates that value be stated in plain language before any delivery mechanism or technology is proposed.

By centralizing these rules at the repo level, skills remain compact and token-efficient, saving context window space.

---

## F. Changes Made

1. **Established Canonical Constitution**:
   Created [`constitution/OAS-CONSTITUTION.md`](../constitution/OAS-CONSTITUTION.md) while maintaining root [`CONSTITUTION.md`](../CONSTITUTION.md) to preserve absolute path compatibility for existing skills (`../../CONSTITUTION.md`).
2. **Created Root `AGENTS.md`**:
   Authored concise, enforceable operating guidelines for all AI agents entering the repository.
3. **Centralized Schema Templates**:
   Established root [`templates/`](../templates/) (`signal_record.md`, `opportunity_card.md`, `ledger_entry.md`) while preserving local copies in `skills/*/templates/` for standalone skill portability.
4. **Established Storage Directories**:
   Created [`opportunities/README.md`](../opportunities/README.md) and [`outputs/README.md`](../outputs/README.md) defining file conventions (`OPP-[YYYYMMDD]-[NN].md`), lifecycle states, and output persistence.
5. **Terminology Unification**:
   Audited and confirmed **Minimal Monetizable Unit (MMU)** as the authoritative constitutional term across all documents.
6. **Updated Root `README.md`**:
   Refined root overview to provide a clear, concise operating summary for humans and agents.

---

## G. Terminology Audit Results

- **Authoritative Term**: **Minimal Monetizable Unit (MMU)**.
- **Source**: Constitution Line 12 explicitly declares: `Core unit: Minimal Monetizable Unit (MMU).`
- **Audit Findings**: The terms "Minimum Meaningful Unit" and "Minimum Movable Unit" appeared only in `TODO.md` review prompts and not in the authoritative Constitution. All active skill definitions and instructions have been verified to standardize on `Minimal Monetizable Unit (MMU)`.

---

## H. Unresolved Founder Decisions (Provisional Working Defaults)

The following parameters are intentionally categorized as **provisional working defaults** requiring founder confirmation rather than immutable constitutional law:

1. **Freshness Verification Windows**:
   - Fast-moving / seasonal claims: **7 days**
   - General SMB pain points: **30 days**
   - Structural or regulatory facts: **90 days**
2. **Research-Depth Pricing Tiers**:
   - Under ~$50: Single pass, single source.
   - ~$50–$500: 2–3 corroborating sources before committing effort.
   - Over ~$500: Buyer conversation required before validation is considered complete.
3. **Graduation Bar**:
   - **3 or more paid instances** of a specific (Problem × Buyer × Solution) triple before proposing productization.
4. **Physical Ledger Format**:
   - Currently standardized as plain Markdown entries in `outputs/` or `opportunities/`. If transactional volume grows, founder may select a database or spreadsheet backend.

---

## I. Architectural Dry-Run Verification

The architecture was evaluated against the five required hypothetical scenarios:

### Scenario A: Seasonal Market Signal
- **Trigger**: Back-to-school spending spike in Kenya.
- **Flow**: `signal-scan` scans within cheap budget, detects fee-payment congestion and inventory gaps, tags evidence as `Sourced` / `Observed`, sets 7-day verify-by date, and outputs a Signal Record.
- **Next Step**: Passes cleanly to `opportunity-scorer`.
- **Result**: **PASS**.

### Scenario B: Founder-Known Problem
- **Trigger**: Founder already has direct intelligence on an artisan business invoicing bottleneck.
- **Flow**: Skips `signal-scan` entirely. Directly enters `opportunity-scorer` at Step 2. Scorer isolates the MMU (e.g., an instant WhatsApp-ready PDF invoice template and M-Pesa ledger), verifies ~72h feasibility, models price ($25–$60), and advises Proceed.
- **Result**: **PASS**.

### Scenario C: Re-evaluation of Stale Opportunity
- **Trigger**: Portfolio review detects an opportunity past its 30-day freshness window.
- **Flow**: `opportunity-ledger` Mode B sweeps the record and flags it `stale — re-verify or kill`. Passes to `opportunity-scorer` in **Update Mode**. Scorer checks current evidence, appends a row to the Re-score history table indicating whether buyer interest and price have strengthened or weakened.
- **Result**: **PASS**.

### Scenario D: Recording a Pursued Opportunity Failure
- **Trigger**: A proposed intervention was pitched but declined by the prospective buyer.
- **Flow**: `opportunity-ledger` Mode A appends a Ledger Entry referencing the card ID. Flags decision as `Declined`, logs buyer outcome (`interested but no`), and extracts the one-sentence learning (Asset principle) to inform future scoring.
- **Result**: **PASS**.

### Scenario E: Graduation Candidate Detection
- **Trigger**: Three distinct small businesses have paid for the same MMU delivery.
- **Flow**: `opportunity-ledger` Mode B groups entries by (Problem × Buyer × Solution) triple. Detects 3 paid instances. Compiles evidence into a graduation dossier in `outputs/graduations/` for founder review. Does *not* auto-build software without founder authorization.
- **Result**: **PASS**.
