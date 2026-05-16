---
title: Governance Layer — [Project / Domain]
phase: H3
status: draft | synthesized | ratified
extracted_from: heuristics/iteration-log.md (cycles N–M)
created: YYYY-MM-DD
last_updated: YYYY-MM-DD
---

# Governance Layer: [Project / Domain]

> **Source of Truth Declaration**
> This document (and its referenced sub-artifacts) is the sole specification for any future implementation. The MVA that generated these insights is deprecated. All architectural decisions, contracts, and invariants below must be re-justified if they are challenged during the rebuild — they are not to be accepted on authority alone.

## 1. Orchestration Specification

### 1.1 Coordination Model

**Chosen Model:** [Central Orchestrator | Event Choreography | Hybrid Saga Orchestrator | Actor Model | ...]

**Rationale (with H2 evidence):**
- Heuristic(s) that drove this decision:
  - [Cycle X] Observation: ...
  - Implication: ...

**Rejected Alternatives (with real reasons they failed in the MVA):**
- Pure choreography — failed because [specific cycle and symptom]
- Central orchestrator with tight coupling — failed because [specific cycle and symptom]

### 1.2 State Machines and Workflow Boundaries

For each major workflow or aggregate:

**Workflow / Aggregate Name:** `kebab-name`

- **States:** (list with descriptions)
- **Transitions:** (from → to, guarded by)
- **Compensation / Rollback Strategy:** (what must happen on failure at each state)
- **Idempotency Requirements:** (at what granularity must this workflow be idempotent?)
- **Exactly-Once vs At-Least-Once:** (and why)

### 1.3 Event Contracts

**Canonical Event Schema Registry** (or reference to schema files):

For each significant event type:

- `EventType`
  - Payload schema (fields + types + optionality)
  - Causation and Correlation ID requirements
  - Ordering guarantees (or lack thereof)
  - Consumer failure semantics (retry, DLQ, poison message handling)
  - Versioning strategy

**Key Discovery:** "We discovered in cycle Y that event ordering must be causal, not merely temporal, because..."

### 1.4 Saga / Compensation Boundaries

- List of sagas with participating services/modules
- Compensation actions (forward or backward recovery)
- Timeout and escalation policies discovered under stress

## 2. Architecture Decision Records (ADRs) — Experience-Backed

Each ADR here must reference the specific iteration cycle(s) and heuristic(s) that produced it. Hypothetical ADRs from H0 are not included unless they were validated or refuted by H2 stress.

**ADR-001: [Decision Title]**

- **Date:** (cycle when decision crystallized)
- **Status:** Accepted | Superseded | Deprecated
- **Context:** What problem were we trying to solve?
- **Decision:** What we chose.
- **Consequences (Positive):** ...
- **Consequences (Negative — Accepted Trade-offs):** ...
- **Evidence from MVA:** Link to iteration log entry or failing run that made this decision inevitable.
- **Rejected Alternatives (with real MVA evidence):**
  - Alternative A — rejected because [specific failure in cycle Z]

(Repeat for each major decision. Aim for 5–12 high-signal ADRs, not dozens of micro-decisions.)

## 3. Observability Governance

### 3.1 Required Signals

**Metrics (what must be measured, with units and aggregation):**
- ...

**Structured Logs (required fields and levels):**
- ...

**Distributed Traces:**
- Correlation ID propagation rules
- Span naming conventions
- Sampling strategy under load

**Business / Domain Events for Observability:**
- ...

### 3.2 Alertable Conditions

For each alertable condition:

- **Symptom** (what the operator sees)
- **Underlying Failure Mode** (from the failure taxonomy)
- **Threshold / Detection Logic**
- **Runbook Link** (or "to be written during rebuild")
- **False Positive / False Negative History** observed in the MVA

### 3.3 "Day One Regret" Retrospective

List of observability capabilities that were painfully missing during H2 iterations. These become non-negotiable requirements for the rebuild.

- "We had no way to correlate a user-visible failure with the specific saga instance..."
- "We could not tell whether a message was retried 3 times or 300 times..."
- ...

## 4. Failure Mode Taxonomy

**Taxonomy Structure:**

| Failure Mode | Blast Radius | Detection Method | Recovery Strategy | Operator Involvement | Evidence from MVA |
|--------------|--------------|------------------|-------------------|----------------------|-------------------|
| ... | (module | workflow | tenant | global) | (log, metric, trace, alert, user report) | (retry, compensation, manual intervention, circuit break) | (none | page | ticket) | (cycle + symptom) |

Populate with every failure mode that was actually experienced and diagnosed during H2. Do not invent hypothetical modes here.

**Critical Insight Example:**
"Transient downstream timeouts at the leaf service level cascaded into saga-level compensation storms because we lacked per-saga rate limiting. This was invisible until we injected latency in cycle 7."

## 5. Interface Contracts & Stable Invariants

**Public Surfaces That Survived Multiple Refactorings:**

- API endpoints / gRPC methods / GraphQL operations
- Event types and their schemas
- State store / repository interfaces
- Configuration and secret contracts

For each, note:
- Why the interface was stable (what would have broken if we changed it)
- Versioning strategy
- Backward compatibility requirements discovered through consumer pain

**Invariants That Must Hold (Regardless of Implementation):**

- "A saga instance must never be considered complete until all compensation actions have either succeeded or been acknowledged as terminal failures."
- "Correlation IDs must be preserved across all async boundaries; loss of correlation is a P0 incident."
- ...

## 6. Cross-Cutting Constraints (Discovered, Not Speculated)

**Security / Authorization:**
- What the MVA revealed about required permission boundaries, token propagation, audit requirements.

**Compliance / Data Residency / Retention:**
- ...

**Performance / Cost / Scale:**
- Real bounds discovered (e.g., "saga throughput collapsed above 120 concurrent instances under our retry policy").

**Multi-Tenancy / Isolation:**
- ...

**Operational / Runbook Requirements:**
- ...

## 7. Heuristics Catalog Reference

Link to the curated, high-confidence subset of heuristics from `heuristics-catalog.md` that directly influenced the governance layer.

Example entry format in the catalog:

```
[Heuristic-042] Workflow Engine Must Be Saga-Idempotent
Cycles: 4, 7, 11
Statement: "The workflow orchestration engine must treat duplicate saga start commands as no-ops at the saga level, not just the task level. Downstream services may see duplicates; the engine must not."
Evidence: "In cycle 7, a retried start command created two parallel saga instances for the same business intent, causing double-billing."
Applies to Rebuild: Mandatory. Any implementation that does not provide saga-level idempotency will re-create this class of failure.
```

## 8. Open Questions and Known Weaknesses

Even after H2 stress, some areas may remain under-explored. Document them here with "minimum stress required to resolve" notes. These become explicit planning debt for the rebuild phase.

## 9. Source and Provenance

- **MVA Location (now deprecated):** `mva/`
- **Iteration Log:** `iteration-log.md` (cycles 1–N)
- **Heuristics Catalog:** `heuristics-catalog.md`
- **Key PRs / Commits / Experiments** during H2 (if applicable)
- **Reviewers who participated in synthesis:** ...

---

**Ratification**

This governance layer was synthesized in H3. It is now the authoritative input for H4 (rebuild planning) and H5 (rebuild execution).

- [ ] Governance layer reviewed by [user / strong model / adversarial reviewer]
- [ ] All major decisions are traceable to specific H2 cycles and heuristics
- [ ] Minimum Viable Stress criteria from the MVA spec have been met and documented

**Date of Synthesis:** YYYY-MM-DD

**Next Phase:** H4 — Sacrificial Throw & Rebuild Planning