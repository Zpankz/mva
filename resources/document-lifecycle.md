# Document Lifecycle

This document describes the precise sequence in which the core documents of the MVA heuristic are created, used, and retired.

---

## The Standard Flow

### Phase 1 — Discovery (MVA Journal)

When facing a high-uncertainty architectural problem, work begins by creating and maintaining a living `MVA.md` journal.

During this phase the agent and user iteratively build a real, runnable architecture while continuously updating the journal with what was tried, what worked, and what did not.

This phase continues until the MVA demonstrates a working shape and sufficient validated understanding exists.

### Phase 2 — Formalization

Once the `MVA.md` journal indicates that a stable architecture has been achieved, its contents are decomposed and formalized into two technical documents:

- `DESIGN.md` — Captures the detailed design decisions and implementation approach.
- `SPEC.md` — Captures the stable requirements, contracts, and behavioral specification.

These two documents represent the "front end" and "back end" technical truth extracted from the MVA experience.

### Phase 3 — Goal Synthesis

A rich `GOAL.md` is then created using the combination of the completed `MVA.md`, `DESIGN.md`, and `SPEC.md`.

This `GOAL.md` carries both clear aspiration and the specific, hard-won practical learnings and anticipated difficulties discovered during the MVA phase.

### Phase 4 — Retirement of the MVA

After `GOAL.md` is finalized, the original `MVA.md` journal is deleted.

Its purpose was discovery. Keeping it risks polluting the clean execution contract with intermediate exploration.

### Phase 5 — Mapping and Execution Preparation

`LAT.md` is updated or expanded after `GOAL.md` exists but before the goal is executed.

Its role is to create clear, linkable mappings between concepts, symbols, and sections so that an agent running the goal has excellent navigational support.

### Phase 6 — Execution

The goal is executed with the backing of `DESIGN.md`, `SPEC.md`, and the mappings in `LAT.md`.

---

## Why This Order Exists

Writing `DESIGN.md` and `SPEC.md` before a real MVA has been built and stressed tends to produce elegant but unvalidated specifications.

Maintaining the MVA journal as a living document forces honesty about what actually worked under real conditions.

Deleting the MVA after `GOAL.md` is created protects the execution phase from contamination by exploratory thinking.

---

*This lifecycle is one of the most important invariants of the MVA heuristic.*