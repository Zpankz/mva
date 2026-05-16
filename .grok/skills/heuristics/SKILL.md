---
name: heuristics
description: >
  Generative Heuristics Planning — inverted empirical planning for high architectural uncertainty.
  Co-create a small runnable Minimally Viable Architecture (MVA), iterate it modularly under real stress
  (evaluation, debugging, refactoring), mine concrete heuristics from the pain, synthesize a unified
  governance layer (orchestration spec + experience-backed ADRs + observability contracts + failure taxonomy),
  then explicitly discard the MVA and rebuild a high-quality production system from the governance truths.
  The entire process is the "plan phase". Use when the correct orchestration model, state boundaries, or
  cross-cutting governance is unknowable through speculation alone. Trigger on: "heuristics", "heuristic plan",
  "generative plan", "plan through scaffolding", "build to discover the architecture", "inverted planning".
  Slash command: /heuristics
---

# Heuristics — Generative Planning Through Sacrificial Scaffolding (Grok Edition)

You are operating under the **Heuristics** planning methodology — an empirical, discovery-driven alternative to speculative document-first planning.

This skill is the Grok-native implementation. It shares the same H0–H5 phase model and artifact formats as the Claude Code version in the parent repository, but is optimized for Grok's context engineering, lean-ctx, and tool use patterns.

## Core Philosophy (Memorize)

Traditional planning asks: "What is the right architecture?"
Heuristics asks: "What architecture reveals itself when we build the smallest possible runnable probe, stress it, and listen to the pain?"

- The MVA is **planning debt**, not product debt. It must be thrown away.
- The **governance layer** (not the MVA code, not the original request) is the source of truth for the rebuild.
- H2 (iteration under stress) is the generative heart. No governance extraction without real failures and evolved cross-cutting concerns.

## The H0–H5 Workflow (Grok Optimized)

### H0 — Framing & MVA Co-Definition
Work with the user to define the smallest runnable system that stresses the 3–7 truly uncertain architectural seams.

**Grok-specific actions:**
- Use `ctx_tree` and `ctx_search` (lean-ctx) for rapid codebase understanding if this is an existing project.
- Capture the MVA spec using the template at `templates/mva-spec.md` in the repo root.
- Explicitly list "Known Technical Debt" in every dimension (persistence, error handling, observability, security, scale).

**Gate:** User must explicitly agree to the MVA scope and the Minimum Viable Stress criteria before you proceed to H1.

### H1 — Scaffold Implementation
Build a working (intentionally imperfect) MVA with clear module boundaries.

**Grok-specific actions:**
- Prefer `ctx_shell` for running commands, tests, and failure injection.
- Mark the entire implementation as sacrificial (`SACRIFICIAL.md` + per-file markers).
- Use lean-ctx aggressively to keep your context window healthy during rapid iteration.

### H2 — Modular Iteration & Heuristic Mining
The most important phase. Enter a tight loop:

**Evolve → Stress (evaluate under load/failure) → Debug → Refactor → Capture Heuristic**

**Grok-specific actions:**
- Maintain a living `iteration-log.md`.
- After every interesting failure or refactor, immediately capture a heuristic in the structured format (see template).
- Actively use failure injection (`ctx_shell` to run load tests, latency injectors, kill processes, etc.).
- Do **not** let the user add product features that are not required to stress the architecture.

**Gate (strict):** You may not move to H3 until:
- At least one non-trivial distributed failure has been diagnosed.
- At least one cross-cutting concern (idempotency, compensation, ordering, observability, etc.) has evolved under pressure.
- 5–15 concrete, evidence-backed heuristics exist in the log.

### H3 — Governance Layer Synthesis
Transform the iteration history into the durable governance artifact.

Use the template at `templates/governance-layer.md`.

**Grok-specific actions:**
- Every claim in the governance layer must be traceable to a specific cycle + heuristic.
- Produce clean Mermaid diagrams for orchestration flows and state machines (Grok is strong at this).
- Pay special attention to the "Day One Regret" observability retrospective — these become non-negotiable requirements for the rebuild.

### H4 — Sacrificial Throw & Rebuild Planning
Explicit ritual:
1. Write `mva/DEPRECATED.md` declaring the MVA dead as a specification source.
2. Generate `rebuild-plan.md` whose **only** inputs are the governance layer + the original problem statement.

The rebuild plan should be high-fidelity enough that a fresh agent can execute it without ever seeing the MVA.

### H5 — Rebuild Execution
Execute the rebuild. This is still "planning" in spirit — you are producing the elegant system as the output of disciplined empirical planning.

## Grok Invocation Patterns

**Primary:**
```
/heuristics <one-line description of the architectural uncertainty or problem>
```

**Special modes:**
- `/heuristics governance-only` — given an existing iteration log, synthesize the governance layer (skip H0–H2).
- `/heuristics extract-heuristics` — given a messy iteration history, produce a clean `heuristics-catalog.md`.

## Artifact Locations (relative to repo root)

```
heuristics/
├── mva-spec.md
├── iteration-log.md
├── heuristics-catalog.md
├── mva/ (sacrificial — never commit runtime state)
├── governance/
│   └── governance-layer.md
└── rebuild-plan.md
```

The templates in `templates/` are authoritative. The Grok skill should read them rather than re-invent the formats.

## Integration with Grok Ecosystem

- Use **lean-ctx** (`ctx_read`, `ctx_shell`, `ctx_search`, `ctx_tree`) heavily during H1 and H2 to stay efficient.
- Record major "why" insights as observations in **thoughtbox** / basic-memory when available.
- The governance layer can later be ingested into knowledge graphs or used as input to other planning skills.
- Works beautifully with `best-of-n` when you need multiple candidate MVA implementations or governance syntheses in parallel.

## Anti-Patterns (Grok Must Enforce)

- Happy-path iteration for more than 2–3 cycles without deliberate failure injection.
- Allowing the user to treat the MVA as a prototype that will "just be cleaned up later."
- Writing heuristics as speculation ("we should probably make the orchestrator idempotent") instead of evidence ("after cycle 7, duplicate start commands created parallel sagas...").
- Skipping the explicit DEPRECATED ritual in H4.

## When to Decline or Pivot

If the user's problem has low architectural uncertainty (clear patterns already exist in the codebase, incremental feature on a well-understood workflow), strongly recommend using a traditional speculative planner (`ce-plan`, `blueprint`, or Grok's native planning) instead. Heuristics has real cost (the MVA) and is only justified when the uncertainty is high.

## Relationship to the Claude Code Version

This Grok skill and the Claude Code skill in the parent directory implement the **same methodology**. They share templates and the phase model. Use whichever harness the user is in for the session. Learnings from either side should be ported back to the canonical `SKILL.md` and templates in the repo.

---

**Begin a session by confirming the user understands this is an empirical, sacrificial, governance-first planning process, then start H0.**