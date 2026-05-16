---
description: Start a Generative Heuristics planning session (inverted planning through sacrificial MVA and heuristic discovery)
---

[HEURISTICS PLANNING MODE ACTIVATED]

$ARGUMENTS

## You are now operating under the Heuristics planning framework.

This is an **inverted, empirical planning process**. The goal of the "plan phase" is not to produce a perfect document up front. The goal is to co-create a small, runnable Minimally Viable Architecture (MVA), subject it to modular iteration and real stress, extract the genuine governance truths from that lived experience, then throw the MVA away and rebuild a high-quality production system from the extracted governance layer.

### The H0–H5 Subphase Structure (This Is Still "Planning")

**H0 — Framing & MVA Co-Definition**
- Work with the user to define the smallest runnable system that stresses the real architectural uncertainties.
- Produce `heuristics/mva-spec.md` with explicit scope, known debt, module contracts, and Minimum Viable Stress criteria.
- Do not proceed until the user agrees the MVA is the right probe.

**H1 — Scaffold Implementation**
- Build the MVA as a working (but deliberately imperfect) executable system.
- Prioritize clear module boundaries over elegance.
- Mark everything as sacrificial.

**H2 — Modular Iteration & Heuristic Mining (The Generative Core)**
- Enter a tight loop: Evolve → Evaluate (under stress) → Debug → Refactor.
- Capture heuristics in the iteration log as they emerge from real pain.
- Do not graduate to H3 until the Minimum Viable Stress gate is passed (non-trivial failures experienced, cross-cutting concerns evolved under pressure, 5–15 concrete heuristics recorded).

**H3 — Governance Layer Synthesis**
- From the iteration history and heuristics, synthesize:
  - Unified orchestration specification
  - Experience-backed ADRs
  - Observability governance
  - Failure mode taxonomy
  - Stable interface contracts and invariants
- This document (`governance/governance-layer.md`) becomes the source of truth for the rebuild.

**H4 — Sacrificial Throw & Rebuild Planning**
- Explicit ritual: mark the MVA as deprecated.
- Produce a high-fidelity rebuild plan whose *only* input is the governance layer (not the original request, not the MVA code).
- The rebuild plan can be handed off to `ce-plan`, `blueprint`, or executed directly.

**H5 — Rebuild Execution**
- Build the production-grade system from the governance layer.
- This is still part of the "plan phase" in spirit — the elegant system is the output of disciplined planning, not the start of "real work."

### Current Phase

You are starting in **H0 (Interview + MVA Co-Definition)**.

Your first actions:
1. Read the full `SKILL.md` and the templates in `templates/` to internalize the methodology.
2. If the user provided a one-line objective in $ARGUMENTS, treat it as the seed. If not, ask for the problem domain and architectural uncertainties.
3. Begin the H0 interview. Ask questions that surface the 3–7 architectural seams that are genuinely uncertain and worth the cost of a sacrificial MVA.
4. Co-create `heuristics/mva-spec.md` using the template. Do not move to H1 until the user explicitly agrees to the scope and the known debt list.

### Important Guardrails

- This is **not** a normal implementation session. The MVA is planning debt.
- You must be rigorous about capturing heuristics from actual iteration pain, not from speculation.
- The "throw it away" moment in H4 is mandatory and psychological as well as technical.
- If at any point the user wants to pivot to a traditional speculative plan (`ce-plan`, `blueprint`, Prometheus), you may do so — but document the decision.

### Artifact Locations (Create as Needed)

```
heuristics/
├── mva-spec.md
├── iteration-log.md
├── heuristics-catalog.md
├── mva/ (sacrificial — will be deprecated)
├── governance/
│   └── governance-layer.md
└── rebuild-plan.md
```

### Transition Commands (User May Say These)

- "Proceed to H1" / "Build the MVA" — after mva-spec is agreed
- "We have enough stress" / "Move to H3" — after Minimum Viable Stress gate
- "Synthesize the governance layer"
- "Throw it away — start the rebuild plan"
- "Exit heuristics mode" (return to normal operation)

---

**Begin the session.**

Greet the user, confirm they understand this is the Heuristics (inverted, generative, sacrificial) planning methodology, and start the H0 interview. Ask the first clarifying question about the architectural uncertainties they want to resolve through this process.