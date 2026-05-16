---
title: MVA Specification — [Short Descriptive Name]
phase: H0
status: draft | agreed
created: YYYY-MM-DD
owner: [user or agent]
---

# MVA Specification: [Project / Domain]

## Purpose

This document defines the **Minimally Viable Architecture (MVA)** — the smallest runnable system whose primary purpose is to stress the architectural seams that are currently uncertain. The MVA is a planning instrument, not a product prototype. It will be discarded after it has served its heuristic discovery role.

## Architectural Questions This MVA Must Answer

List the 3–7 core uncertainties that justify using the Heuristics methodology:

1. **Orchestration Model** — [e.g., "Should we use a central orchestrator or event choreography for the multi-step approval workflow?"]
2. **State Machine Boundaries** — [e.g., "Where do saga boundaries lie when compensation can be partial?"]
3. **Observability Requirements** — [e.g., "What correlation and causation signals are actually required to debug distributed failures under load?"]
4. ...

## MVA Scope (What Is In)

- Core modules/components that must exist for the seams to be real:
  - `module-a` — purpose + primary contract
  - `module-b` — purpose + primary contract
  - ...

- Primary execution paths that must be runnable end-to-end (happy path + 1–2 interesting failure injections):
  - Path 1: ...
  - Path 2: ...

- Minimum instrumentation / logging / tracing necessary to observe the behavior under stress.

## Explicit Technical Debt & Simplifications (What Is Intentionally Omitted or Weakened)

This list is critical. Every item here is a known compromise that will be revisited in the rebuild.

- **Persistence**: In-memory only / SQLite file / no durability guarantees
- **Error Handling**: Naive retries, no circuit breakers, no dead-letter queues
- **Security / Auth**: Mock tokens, no real RBAC, single-tenant assumption
- **Observability**: Basic logging only; no distributed tracing, no metrics aggregation
- **Performance / Scale**: Single-process, no connection pooling, no backpressure
- **Resilience**: No idempotency keys at workflow level, at-most-once delivery
- **Deployment**: Local only, no containerization, no configuration management
- **Other**: ...

## Module Inventory and Contracts

For each module, define:

**Module Name:** `short-kebab-name`

- **Responsibility (one sentence)**
- **Primary Inputs** (events, API calls, commands)
- **Primary Outputs** (events emitted, side effects, state changes)
- **State Machine(s)** (if any) — high-level states and transitions
- **Known Interface Assumptions** (what we are pretending is stable for the MVA)

## Minimum Viable Stress Criteria (Graduation Gate for H2)

The MVA is not ready for governance extraction until it has experienced:

- [ ] At least one non-trivial, distributed failure mode that required diagnosis across modules.
- [ ] At least one cross-cutting concern (retry, idempotency, ordering, compensation, observability) that evolved under pressure and revealed coupling.
- [ ] Measurable evidence that the current module boundaries are either adequate or need to change (document the evidence).
- [ ] A living `iteration-log.md` containing 5–15 concrete heuristics captured during H2 cycles.

## Success Signals for the MVA (How We Know It Served Its Purpose)

- We can articulate why the orchestration model must be X rather than Y, backed by specific iteration cycles.
- We have discovered at least N invariants or failure modes that were invisible during H0.
- The team/agent has high confidence that a rebuild from the governance layer will avoid the majority of the pain experienced in the MVA.

## Out of Scope for This MVA (Will Be Addressed in Rebuild or Later)

- Any product feature not required to exercise the architectural seams.
- Production deployment, scaling, multi-region, compliance, etc.
- Polish, UX, performance tuning.

## Known Risks of This MVA Approach

- Risk that the MVA becomes too lovable and we resist throwing it away (mitigation: explicit DEPRECATED ritual in H4).
- Risk that we under-stress the system and produce a weak governance layer (mitigation: Minimum Viable Stress gate).
- Risk that useful MVA code leaks into the rebuild without re-justification (mitigation: governance layer is the only source of truth for H4/H5).

---

**Agreement**

- [ ] User / Stakeholder has reviewed and agrees this MVA scope is sufficient to answer the architectural questions.
- [ ] Agent / Planner confirms the scope is small enough to implement in a reasonable planning-time budget.

**Date of Agreement:** YYYY-MM-DD

**Next Phase:** H1 — Scaffold Implementation (build the MVA defined above)