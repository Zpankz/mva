# Using the Heuristic

This document explains the practical steps for applying the MVA heuristic to a new high-uncertainty architectural problem.

---

## When to Use This Methodology

The MVA heuristic is appropriate when the correct orchestration model, state boundaries, or cross-cutting governance for a system is genuinely uncertain and the cost of discovering the wrong shape in production is high.

It is not intended for incremental work on well-understood patterns.

---

## Step-by-Step Process

### 1. Preparation

Read `AGENTS.md`, `LAT.md`, and `SKILL.md` at the root of this repository (or the equivalent in your local copy).

Copy the four templates from `templates/` into the root of the target project.

### 2. Discovery Phase (MVA Journal)

Begin active work on the architecture while maintaining `MVA.md` as a living journal.

Add new cycles as iteration progresses. Record both what worked and what did not with honesty.

Continue until the MVA demonstrates a working architecture and clear, validated learnings exist.

### 3. Formalization Phase

Once the `MVA.md` journal is considered complete, decompose its contents into `DESIGN.md` and `SPEC.md`.

These documents should be precise, stable, and free of exploratory narrative.

### 4. Goal Synthesis

Create `GOAL.md` using the completed `MVA.md` together with the new `DESIGN.md` and `SPEC.md`.

The resulting `GOAL.md` should contain clear aspiration, motivation, specific learnings from the MVA, and realistic anticipated difficulties.

### 5. Retirement and Mapping

Delete the original `MVA.md`.

Update or expand `LAT.md` to include any new symbols, definitions, or relationships discovered during the engagement.

### 6. Execution

Run the goal with the support of `DESIGN.md`, `SPEC.md`, and the mappings in `LAT.md`.

---

## Best Practices

- Treat `MVA.md` as a journal, not a plan. Update it in real time.
- Do not rush formalization. Weak MVAs produce weak `DESIGN.md` and `SPEC.md`.
- Be explicit about what was learned from failure, not only from success.
- After the goal is created, invest in `LAT.md` mappings before execution begins.

---

*Following this process consistently is what separates high-quality architectural outcomes from elegant but fragile specifications.*