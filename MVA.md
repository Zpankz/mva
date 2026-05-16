# MVA

**Minimally Viable Architecture — Specification and Examples**

This document defines what constitutes a valid Minimally Viable Architecture (MVA) for the Heuristics methodology and provides canonical examples.

---

## Purpose

An MVA is not a prototype, not a vertical slice, and not "the real thing with some corners cut."

An MVA is the **smallest runnable system** whose explicit purpose is to make the currently uncertain architectural seams *real and stressable*.

Every MVA must be traceable back to a specific set of architectural questions that were unknown at H0 time.

---

## Required Properties of Any Valid MVA

### 1. Scope is Question-Driven
The MVA's boundaries are defined by the architectural uncertainties, not by product features.

Example good scope:
> "We need to discover the correct saga boundary and compensation strategy for a multi-party medical workflow approval process."

Example bad scope:
> "Build the first version of the medical workflow system."

### 2. Known Debt is Explicit
Every MVA must declare, in writing, the technical simplifications it is *intentionally* accepting in each dimension:

- Persistence model (and why it is acceptable for discovery)
- Error handling / retry model
- Security / authorization model
- Observability model
- Deployment / runtime model
- Concurrency / isolation model

### 3. Module Boundaries are Clear and Replaceable
It must be obvious which code belongs to which conceptual module, and it must be feasible to replace one module's implementation without rewriting the others.

### 4. Minimum Viable Stress Criteria are Defined Upfront
Before H1 begins, the MVA spec must define what "enough stress" looks like for *this* MVA. This is the graduation gate from H2 to H3.

---

## Anti-Patterns

- Adding product features "while we're at it" that are not required to stress the target seams.
- Optimizing or polishing the MVA (premature elegance).
- Treating the MVA as something that "might be good enough to evolve into production."
- Vague debt declarations ("we'll simplify auth").

---

## Canonical MVA Example (Heuristics Itself)

When we built the first version of the Heuristics skill, the MVA was:

- A single-process, in-memory event bus
- No real persistence (or minimal SQLite)
- Naive retry with no circuit breaking
- Mock authentication
- Basic console logging only
- Single-tenant assumption

The explicit architectural questions being probed were:
- Correct granularity of saga boundaries for planning workflows
- How much of the governance layer can be synthesized vs must be authored
- What "Minimum Viable Stress" actually feels like in practice for a planning methodology

This MVA was deliberately thrown away after H4.

---

## Relationship to Templates

The authoritative template for writing an MVA spec lives at:

`templates/mva-spec.md`

Every real Heuristics engagement should begin by producing a filled-out version of that template.