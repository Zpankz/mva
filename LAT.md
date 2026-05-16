# LAT

**Living Architecture Trace for the MVA Heuristic**

This document follows `lat.md` authoring conventions. Every section begins with a leading paragraph that establishes its identity.

---

## Purpose of This Document

`LAT.md` serves as the structured, cumulative knowledge graph for the MVA heuristic methodology.

It captures discoveries, refinements, meta-heuristics, and cross-document mappings that emerge from real usage. Agents consult this file to understand how the methodology actually behaves in practice, rather than relying solely on initial specifications.

---

## Position in the Document Lifecycle

`LAT.md` is maintained **after** a `GOAL.md` has been created but **before** that goal is executed in production.

Its primary role is to map symbols, definitions, concepts, and relationships so that an agent running the `GOAL.md` has reliable, navigable access to the underlying knowledge.

---

## Core Concepts

### Heuristic

A concrete, evidence-backed observation about what worked or failed during the construction and validation of a Minimally Viable Architecture.

Every entry in this document should eventually trace back to a specific cycle or decision recorded in a project's `MVA.md`.

### Governance Layer Evolution

Changes to the expected structure, sections, or invariants of a governance layer that have been validated across multiple real MVA engagements.

### Phase Gate Refinement

Adjustments to the strictness, ordering, or exit criteria of the MVA heuristic phases, driven by practical experience rather than theory.

---

## Discovered Heuristics

### The Living Journal Nature of MVA.md Is Essential

Recording failures, pivots, and moments of confusion in `MVA.md` produces significantly higher-quality `DESIGN.md`, `SPEC.md`, and `GOAL.md` than recording only successes.

**Implication:** Agents must be encouraged to write honestly in the MVA journal, including dead ends and reversals.

### Formalization Should Not Happen Too Early

Decomposing an incomplete or weakly stressed `MVA.md` into `DESIGN.md` and `SPEC.md` tends to lock in fragile assumptions.

**Implication:** The transition from MVA to formal documentation should be gated by clear evidence that a stable, working architecture has emerged.

---

## Cross-Document Mappings

This section will be expanded with `[[wiki links]]` to specific sections in `MVA.md`, `SPEC.md`, `DESIGN.md`, and `GOAL.md` as the methodology matures through use.

Example future entries:
- `[[mva#Cycle 007]]` produced the insight that eventually became the retry policy in `[[spec#Error Handling]]`.
- The structure of `[[goal#Anticipated Difficulties]]` is derived from patterns observed across multiple `MVA.md` journals.

---

## How to Contribute New Entries

When a real engagement using the MVA heuristic produces a meaningful discovery:

- Add a new top-level section with a clear heading.
- Begin the section with a concise leading paragraph.
- Include concrete evidence (project, cycle, or decision).
- State the implication for future use of the methodology.
- Use `[[ ]]` wiki links to connect the insight to other documents where appropriate.

---

*This document grows through use. Its value increases as more real MVA journals are completed and their learnings are mapped.*