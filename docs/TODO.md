You are now the **Repository Architect and Integration Agent** for the Opportunity-to-Asset System (OAS).

The repository you are working in contains the work produced by Claude Sonnet 5 after analyzing the OAS Constitution and designing the initial Skill architecture.

Your job is **NOT to redesign OAS**.

Your job is to take the existing files, understand the architecture they already establish, and turn them into a clean, coherent, canonical repository that can later be used by Codex, Claude Code, Antigravity, and other coding agents.

Repository:
`https://github.com/Suyanka21/Opportunity-to-Asset-System.git`

You are already operating inside the repository environment. Inspect the repository as it currently exists before making any changes.

---

# 1. PRIMARY OBJECTIVE

Transform the current repository into the canonical **OAS Agent Operating Repository**.

The repository must clearly communicate:

* what OAS is
* what governs OAS
* what global instructions apply to every agent session
* what Skills exist
* when each Skill is invoked
* what artifacts each Skill consumes and produces
* how state moves through the system
* where opportunity records live
* where reusable templates/reference material lives
* how an agent should work with the repository
* how another agent can understand the system without asking the founder basic structural questions

The final repository should be understandable by a capable coding agent opening the repository for the first time.

---

# 2. AUTHORITATIVE MATERIAL

Treat the following as the hierarchy of authority:

1. The founder-supplied OAS Constitution
2. The existing Claude-created OAS Skill architecture
3. Existing Skill files and templates
4. Repository organization and implementation details

Do NOT allow repository organization to change the principles of the Constitution.

Do NOT silently rewrite the Constitution.

Do NOT invent constitutional rules.

If you discover an apparent contradiction between the Constitution and a Skill, preserve the Constitution and flag the contradiction in your final report.

---

# 3. PRESERVE CLAUDE'S CORE ARCHITECTURE

Claude's current decomposition is:

### Skill 1 — `signal-scan`

Purpose:

* observe
* detect
* capture real-world signals
* produce Signal Records

### Skill 2 — `opportunity-scorer`

Purpose:

* validate
* isolate the Minimum Meaningful/Movable Unit terminology already established in the repository
* estimate commercial value
* assess the 72-hour constraint
* determine whether an opportunity deserves progression
* support re-scoring/update mode for existing opportunities

Produces:

* Opportunity Cards

### Skill 3 — `opportunity-ledger`

Purpose:

* record evidence
* preserve opportunity history
* identify repetition
* support review
* support graduation decisions

Produces:

* Ledger Entries
* Review Summaries

This three-Skill architecture is intentional.

**Do not expand it into a large collection of Skills simply because additional concepts exist in the Constitution.**

If a concept can appropriately live in:

* `GLOBAL_AGENT_INSTRUCTIONS.md`
* a template
* a reference document
* a Skill mode
* repository orchestration

then prefer that over creating another Skill.

Only propose a new Skill if you discover a genuine independent capability that cannot reasonably belong in the existing architecture.

---

# 4. GLOBAL AGENT INSTRUCTIONS

Inspect the existing `GLOBAL_AGENT_INSTRUCTIONS.md`.

It is intended to contain cross-cutting rules such as:

* human decision authority
* Kenya-first default
* evidence taxonomy

  * Observed
  * Sourced
  * Inferred
  * Hypothesis
* evidence freshness
* research-depth-by-value
* other rules that should be loaded once rather than duplicated across Skills

Preserve this architecture.

Do not duplicate large portions of these instructions inside every SKILL.md.

Optimize for agent context efficiency.

---

# 5. REPOSITORY ORGANIZATION

Inspect the current files first.

Then establish a clean structure along these lines where appropriate:

```text
/
├── AGENTS.md
├── README.md
├── GLOBAL_AGENT_INSTRUCTIONS.md
├── constitution/
│   └── OAS-CONSTITUTION.md
│
├── skills/
│   ├── signal-scan/
│   │   └── SKILL.md
│   ├── opportunity-scorer/
│   │   └── SKILL.md
│   └── opportunity-ledger/
│       └── SKILL.md
│
├── templates/
│   ├── ...
│
├── opportunities/
│   └── README.md
│
├── outputs/
│   └── README.md
│
└── docs/
    └── ...
```

This is a proposed organizational model, not a command to blindly create every directory.

**Only create directories/files that are justified by the existing architecture.**

Do not create empty scaffolding simply for appearance.

---

# 6. ROOT AGENTS.MD

Create or refine the root `AGENTS.md`.

It should explain how an agent entering this repository should operate.

At minimum it should establish:

1. Read the Constitution first.
2. Read `GLOBAL_AGENT_INSTRUCTIONS.md`.
3. Understand the available Skills.
4. Do not bypass lifecycle controls.
5. Do not fabricate evidence.
6. Do not invent market data.
7. Do not silently change constitutional rules.
8. Keep outputs in the repository.
9. Preserve auditable state.
10. Respect the 72-hour discipline.
11. Treat the founder as the final commercial decision-maker.
12. Prefer minimal context and minimal unnecessary work.

The root AGENTS file should be concise.

Do not copy the entire Constitution into it.

---

# 7. SKILL FILES

Inspect all three existing Skills carefully.

For each Skill verify:

* valid Agent Skills frontmatter
* clear name
* clear description
* clear trigger
* clear inputs
* clear outputs
* clear procedure
* clear stop/failure conditions
* correct references to repository files
* no broken paths
* no duplicated constitutional material
* no unnecessary verbosity
* no hidden assumptions that contradict the Constitution

Do not rewrite a Skill merely to make it stylistically prettier.

Only make changes where necessary for:

* correctness
* consistency
* portability
* discoverability
* broken references
* ambiguity that would cause an agent to execute incorrectly

---

# 8. TERMINOLOGY AUDIT

Perform a repository-wide terminology audit.

In particular, inspect the distinction between:

* Minimum Meaningful Unit
* Minimum Movable Unit
* MMU

The repository must use one canonical term consistently.

Do NOT choose the correct term based on your own preference.

Determine which terminology is authoritative from the Constitution and existing OAS source material.

If the source material itself is genuinely ambiguous, do not silently decide.

Document the ambiguity in the final audit report and preserve the source wording until the founder resolves it.

---

# 9. PATH AND REFERENCE AUDIT

Check every internal reference.

Examples:

* Constitution paths
* Skill references
* template references
* opportunity record references
* README references
* AGENTS references
* relative paths inside SKILL.md files

No Skill should depend on a path that does not exist.

No documentation should point to a file that was moved without updating the reference.

---

# 10. DO NOT INVENT NUMERIC RULES

Claude identified several values that were deliberately invented as working defaults rather than derived from the Constitution:

* 7-day freshness
* 30-day freshness
* 90-day freshness
* <$50 research tier
* $50–500 research tier
* > $500 research tier
* 3 paid instances as a graduation threshold

These are explicitly identified as founder decisions still requiring judgment.

Do NOT silently convert these into immutable OAS rules.

Preserve them only if the current repository already stores them as configurable working defaults.

If they need to be clearly labelled as provisional, do so.

The distinction must remain:

**constitutional rule ≠ working default ≠ founder decision pending**

---

# 11. DO NOT BUILD THE PRODUCT

This repository is currently the operating architecture for OAS.

Do NOT:

* build a web application
* build a dashboard
* build a database
* build authentication
* build an API
* build a frontend
* create a SaaS product
* connect external services
* perform a market scan
* generate real opportunities
* spend effort researching Kenya's economy
* create the eventual customer-facing Opportunity Intelligence product

Those are later phases.

Right now we are building the underlying operating system.

---

# 12. VALIDATION

After organizing the repository, perform a structural validation.

Check:

### Architecture

* Can a new agent understand the system?
* Are the three Skills discoverable?
* Is there one clear authority hierarchy?
* Is state represented consistently?
* Is lifecycle ownership clear?

### Skills

* Are all SKILL.md files valid?
* Are names and descriptions clear?
* Are triggers unambiguous?
* Are inputs and outputs defined?
* Are failure conditions defined?

### Integrity

* Are constitutional rules preserved?
* Are evidence standards preserved?
* Is human authority preserved?
* Is the 72-hour rule preserved?
* Is the commercial orientation preserved?

### Repository

* Are paths valid?
* Are references valid?
* Are there orphaned files?
* Are there duplicate instructions?
* Are there unnecessary files?
* Is the structure minimal?

---

# 13. CREATE A REPOSITORY ARCHITECTURE REPORT

Create a concise file:

`docs/REPOSITORY_ARCHITECTURE.md`

It should document:

### A. Final repository structure

Show the final tree.

### B. Authority hierarchy

Explain which files outrank which.

### C. Skill map

For each Skill:

* purpose
* trigger
* input
* output
* lifecycle role

### D. State flow

Explain how information moves:

Signal → Opportunity → Evaluation → Ledger → Review/Graduation

### E. Global instructions

Explain what belongs in `GLOBAL_AGENT_INSTRUCTIONS.md` and why.

### F. Changes made

List only substantive changes.

### G. Unresolved founder decisions

List anything you intentionally did not decide because it requires founder judgment.

Do not turn unresolved questions into invented rules.

---

# 14. README

Create or refine `README.md`.

It should give a new agent/human a fast explanation of:

* what OAS is
* why it exists
* its core operating principle
* the three Skills
* the role of the Constitution
* the role of the global instructions
* how the repository is organized
* what the repository is NOT yet

Keep it concise.

This is an operating repository, not a marketing brochure.

---

# 15. TEST THE ARCHITECTURE

Perform a lightweight structural dry run using hypothetical examples only.

Do NOT perform actual market research.

Test:

### Scenario A

A seasonal market signal is discovered.

Verify that it can enter through `signal-scan` and reach `opportunity-scorer`.

### Scenario B

The founder already knows about a small business problem.

Verify that it can enter the appropriate point without violating lifecycle rules.

### Scenario C

An existing opportunity needs to be re-evaluated because evidence has become stale or changed.

Verify that `opportunity-scorer` can operate in update/re-score mode and that `opportunity-ledger` preserves the history.

### Scenario D

A previously pursued opportunity failed.

Verify that the system records the failure rather than losing it.

### Scenario E

Repeated paid delivery suggests that something may deserve graduation.

Verify that the ledger can preserve the evidence required for that decision.

The dry run is architectural only.

Do not invent market facts.

---

# 16. TOKEN/CONTEXT EFFICIENCY

This repository will eventually be used by constrained AI agents.

Therefore:

* prefer concise instructions
* avoid duplicated rules
* avoid giant README files
* avoid repeating the Constitution
* avoid unnecessary references
* avoid creating Skills for every small operation
* use progressive disclosure where useful
* keep the hot path small
* make expensive work conditional on earlier evidence

The repository should be optimized for **agent execution**, not documentation volume.

---

# 17. GIT DISCIPLINE

Before committing:

1. Inspect the existing repository state.
2. Make the minimum necessary changes.
3. Review the resulting file tree.
4. Review the important diffs.
5. Ensure no secrets or credentials are present.
6. Ensure no generated junk is committed.
7. Ensure all references resolve.
8. Ensure the repository is internally coherent.

Then create the **first canonical commit** for the OAS repository.

Use a clear commit message such as:

`feat: establish canonical OAS agent architecture`

Do not create multiple speculative commits.

---

# 18. FINAL RESPONSE

After completing the repository work, report:

1. Final repository structure
2. Files created
3. Files moved
4. Files materially changed
5. Validation results
6. Dry-run results
7. Any unresolved founder decisions
8. Commit hash
9. Confirmation that the repository is ready for the next OAS development phase

Do not claim the OAS system is fully built.

The objective of this task is to establish the **canonical agent architecture and repository foundation**.

Begin by inspecting the repository and existing files.

Do not ask me to manually reproduce files that are already present in the repository.
