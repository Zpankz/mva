---
lat:
  require-code-mention: false
---

# MVA — MVA Heuristic Document System

**Status:** In Progress  
**Started:** 2026-05-16  
**Last Updated:** {{CURRENT_DATE}}  
**Owner:** Grok (in collaboration with user)

---

## Purpose

This document is the living journal for the development of the MVA heuristic itself.

It records the iterative process of discovering what `MVA.md` should be as a first-class, peer-level document in the set that includes `AGENTS.md`, `LAT.md`, `SPEC.md`, `DESIGN.md`, and `GOAL.md`.

The goal is to design `MVA.md` such that it functions effectively as a dynamic, progressively written journal during real architectural discovery work.

---

## Starting Context

The project began with a desire to invert traditional planning by using a sacrificial, runnable MVA to generate real architectural understanding before producing formal specifications and goals.

Early documents treated `MVA.md` primarily as a template or example. Through discussion, it became clear that `MVA.md` must instead be a **living journal** of what worked and what did not during active iteration.

This realization elevated `MVA.md` to the status of a core heuristic document on equal footing with the others.

---

## Cycle 001 — Clarifying the Role of MVA.md — 2026-05-16

**Hypothesis going into this cycle:**

`MVA.md` should be a structured template that agents fill out once, similar to other planning documents.

**What was tried:**

Multiple versions of `MVA.md` were written with varying levels of formality, some closer to a spec and some closer to a journal.

**What worked:**

The explicit statement that `MVA.md` is a "living journal of what worked and what didn't until a real MVA is achieved" provided immediate clarity.

**What didn't work / Pain points:**

Treating `MVA.md` as a static or pre-filled document conflicted with the fundamental idea of generative, empirical discovery through iteration.

**Key insight:**

`MVA.md` is not the output of planning. It *is* the planning process, captured in real time.

**Updated direction:**

Design `MVA.md` primarily as an iterative journal that follows `lat.md` conventions, supports progressive writing during work, and is only later decomposed into `DESIGN.md` and `SPEC.md`.

---

## Current State of the MVA

The current working understanding is that `MVA.md` should:

- Be written dynamically while building and stressing a real architecture.
- Follow `lat.md` section rules (leading paragraphs, clear identity).
- Record both successes and failures honestly.
- Serve as the primary source from which `DESIGN.md`, `SPEC.md`, and eventually `GOAL.md` are derived.
- Be deleted once `GOAL.md` is finalized.

Templates for `MVA.md`, `SPEC.md`, `DESIGN.md`, and `GOAL.md` have been created in `templates/` to support this workflow.

---

## Remaining Areas of Uncertainty

- What is the ideal granularity and rhythm for adding new cycles to a `MVA.md` journal during active work?
- How much structure should be enforced in `MVA.md` versus allowing more free-form narrative when it better captures the lived experience?
- How should agents be instructed (via `SKILL.md` and `AGENTS.md`) to maintain the journal without it becoming burdensome?

---

## Next Steps

Continue refining the `MVA.md` template and the supporting instructions in `SKILL.md` and `AGENTS.md` while applying the heuristic to real problems.

The next significant cycle will likely involve using the current `MVA.md` template on an actual high-uncertainty architectural problem and observing what needs to change.

---

*This document is itself an instance of the MVA heuristic in action. It will continue to evolve until the architecture of `MVA.md` as a first-class document feels stable and well-understood.*