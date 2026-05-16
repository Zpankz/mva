# Templates for the MVA Heuristic Document System

This directory contains the canonical, reusable templates for the core documents in the **MVA** (Minimally Viable Architecture) heuristic methodology.

These templates are designed to be used when applying the Heuristics process to a new high-uncertainty architectural problem.

## Document Lifecycle (Important)

The correct flow is:

1. **MVA.md** — Written *first* and *iteratively* as a living journal while you and the agent build and stress a real, working MVA. This is the primary discovery artifact.
2. **DESIGN.md + SPEC.md** — Created *after* `MVA.md` is considered complete. These formalize the technical implementation (front-end and back-end) by decomposing the learnings from the MVA.
3. **GOAL.md** — Synthesized from the combination of the completed `MVA.md` + `DESIGN.md` + `SPEC.md`. This becomes the executable contract.
4. **MVA.md is deleted** (sacrificial).
5. **LAT.md** is updated/expanded *after* `GOAL.md` exists but *before* the goal is executed, to provide a clean, linkable knowledge graph for the agent.

## How to Use These Templates

- Copy the relevant template into the root of your target project (or the appropriate location).
- Replace all `{{VARIABLE_NAME}}` placeholders with concrete content.
- Follow `lat.md` conventions in the resulting files:
  - Every section (`##`, `###`, etc.) **must** begin with a leading paragraph (ideally ≤250 characters) that gives the section its identity.
  - Use `[[wiki links]]` for cross-references between documents and sections.
  - Keep sections focused and agent-navigable.

## Template Overview

| Template | Purpose | When to Use | Style |
|----------|---------|-------------|-------|
| `MVA.md` | Living journal of iteration ("what worked / what didn't") | During the active discovery and MVA-building phase | Iterative, journal-style, `lat.md` conventions |
| `SPEC.md` | Formal, stable technical specification | After `MVA.md` is validated and complete | Structured, precise, `lat.md` conventions |
| `DESIGN.md` | Detailed technical design and implementation approach | After `MVA.md` is validated and complete | Technical depth, `lat.md` conventions |
| `GOAL.md` | Rich executable contract for long-running work | After `MVA.md` + `SPEC.md` + `DESIGN.md` exist | Aspirational + practical, includes motivation, learnings, and anticipated difficulties |

## MVA.md Generation Style

The `MVA.md` template is specifically designed to support an **iterative, file-based planning pipeline** (in the spirit of tools like `planning-with-files`).

You (or the agent) should:
- Add new `### Cycle N` sections as work progresses.
- Continuously update the "Current State of the MVA", "Decision Log", and "Criteria for MVA Completion" sections.
- Treat the document as a living record rather than a one-time plan.

Once the MVA is achieved, stop updating `MVA.md` and begin the decomposition into `DESIGN.md` and `SPEC.md`.

## Variables

All templates use `{{VARIABLE_NAME}}` placeholders. Common variables across templates include:

- `{{PROJECT_OR_FEATURE_NAME}}`
- `{{DATE}}`
- `{{AGENT_OR_PERSON}}`

Fill these in as early as possible when starting a new engagement.

## Best Practices

- Keep `MVA.md` honest — record failures and pivots, not just successes.
- Do not rush the transition from `MVA.md` to `DESIGN.md`/`SPEC.md`. The quality of the later documents depends on the depth of the MVA journal.
- After creating `GOAL.md`, delete the `MVA.md` (or archive it) and generate the supporting `LAT.md` mappings before execution begins.

These templates are living artifacts. Improve them as the methodology itself evolves through real use.