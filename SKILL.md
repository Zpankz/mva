---
name: heuristics
description: >
  Inverted planning framework that treats the "plan phase" as a generative heuristic discovery process.
  Co-create a Minimally Viable Architecture (MVA) — a deliberately imperfect but runnable sacrificial system —
  then iterate modularly through evaluation, debugging, and refactoring to extract a unified orchestration spec,
  architecture decisions, and observability governance layer. The MVA is then thrown away, and a high-quality
  production system is rebuilt from the extracted governance truths. Use when architectural uncertainty is high
  and the correct shape of orchestration, state, and observability is only knowable through lived stress.
  TRIGGER when: user says "heuristics", "heuristic plan", "generative plan", "plan through scaffolding",
  "build to discover", "inverted plan", or describes a complex system where "we don't know the right architecture yet".
  This skill is the planning phase; the output is governance + rebuild plan, not a finished product.
origin: ideas/heuristics
---

# Heuristics — Generative Planning Through Sacrificial Scaffolding

**Heuristics** is a planning methodology that inverts the dominant "plan first, build once correctly" paradigm.

## Core Inversion

Traditional planning (Prometheus, `ce-plan`, `blueprint`) is **speculative**:
- Research → Interview → Synthesize → Produce high-fidelity implementation document
- Execution happens later, against the document
- Risk: the plan is only as good as the planner's foresight

**Heuristics** is **empirical and generative**:
- Co-define a Minimally Viable Architecture (MVA) — the smallest runnable system that stresses the real architectural seams
- Implement the MVA as a working (but intentionally flawed) system
- Iterate modularly: evolve → evaluate → debug → refactor
- Mine **heuristics** (empirical truths) from the lived experience of the system under stress
- Synthesize a **unified governance layer** (orchestration spec + ADRs + observability contracts + failure taxonomy)
- Explicitly discard the MVA
- Rebuild the production-grade system from the governance layer

The entire H0–H5 process is still the **planning phase**. The "plan" artifact is the governance layer + the rebuild plan + the recorded heuristics. The elegant production system is the *output of planning*, not the beginning of implementation.

## When to Use Heuristics

Use this framework when **one or more** of the following are true:

- The correct orchestration model (choreography vs orchestration, saga boundaries, compensation strategy) is genuinely uncertain
- Novel state machines, distributed workflows, or multi-party coordination where failure modes and invariants are not yet known
- Observability and governance requirements are cross-cutting and only become visible under realistic load or failure injection
- The team (or agent) has strong domain intuition but weak architectural precedent in the codebase
- The cost of building the "wrong" production architecture is high, and the cost of a throwaway MVA is acceptable
- You want the final architecture to be *post-experience* rather than *pre-speculation*

**Do NOT use** when:
- The work is incremental on a well-understood pattern (use `ce-plan` or `blueprint`)
- The primary risk is product definition, not architecture (use `ce-brainstorm`)
- The task is small, well-bounded, or can be confidently specified without execution feedback
- You cannot afford even a small throwaway system (time, cost, or political constraints)

## Philosophy and Guardrails

1. **Sacrificial by Design** — The MVA is planning debt, not technical debt. It must be explicitly marked and eventually deleted. Any code that survives into the final rebuild does so only because it was re-justified against the governance layer.

2. **Modularity as a Planning Primitive** — The MVA must be built with clear module boundaries so that iteration can proceed with minimal coupling. Interface stability during H2 is a primary success signal.

3. **Heuristics Over Hypotheses** — Every significant architectural claim in the governance layer must be traceable to a specific iteration cycle, failure, or refactoring insight. "We think X will be important" is not a heuristic. "After three iterations, retry semantics leaked into every consumer, forcing us to make the workflow engine idempotent at the saga level" is a heuristic.

4. **Governance Layer is the Source of Truth** — The rebuild plan (H4/H5) is derived from the governance layer, not from the original user request or the MVA code. The MVA is evidence; the governance layer is the specification.

5. **Minimum Viable Stress** — H2 is not complete until the MVA has experienced meaningful failure modes, load, or edge conditions. Happy-path iteration alone is insufficient to graduate to H3.

6. **Explicit Throw Ritual** — There must be a deliberate moment where the MVA is marked deprecated and the team/agent commits to the rebuild. This is a psychological and process boundary, not an afterthought.

## The H0–H5 Subphase Workflow

### H0: Framing & MVA Co-Definition (Collaborative)

**Goal:** Establish a shared, explicit contract for the smallest runnable system that will exercise the architectural questions that matter.

**Activities:**
- Interview the user (or requirements) to surface the 3–7 core architectural seams, state machines, or integration boundaries that are uncertain.
- Define the MVA scope as "just enough to make those seams real and runnable."
- Explicitly enumerate the technical debt and simplifications that are *acceptable* in the MVA (e.g., "in-memory event bus", "no persistence", "naive retry", "single-tenant only").
- Name the modules/components and their primary contracts (event schemas, API signatures, state machine definitions).
- Define "minimum viable stress" criteria for graduation from H2.

**Exit Criteria:**
- `mva-spec.md` exists and is agreed upon.
- The MVA is small enough to implement in hours/days, not weeks.
- The "known debt" list is explicit and non-controversial.

**Artifact:** `heuristics/mva-spec.md` (see templates)

### H1: Scaffold Implementation

**Goal:** Produce a working, executable MVA that implements the contracts defined in H0.

**Constraints:**
- Prioritize modularity and interface clarity over elegance or performance.
- Every major component should be replaceable without rewriting the rest of the system.
- Mark the entire MVA as sacrificial (directory `mva/`, `SAC RIFICIAL.md` markers, or equivalent).
- Do not optimize prematurely. The goal is *survivability under iteration*, not production readiness.

**Exit Criteria:**
- The MVA runs end-to-end for the primary happy path(s) defined in the mva-spec.
- Module boundaries are clear enough that a subsequent agent can evolve one module with confidence.

### H2: Modular Iteration & Heuristic Mining (The Generative Loop)

This is the heart of the methodology. The agent and user enter a tight loop:

**Cycle Structure (repeat until Minimum Viable Stress is achieved):**
1. **Select** a module, contract, or cross-cutting concern to evolve.
2. **Evolve** it (add behavior, change implementation, introduce a new seam).
3. **Evaluate** under realistic conditions (manual test, scripted load, failure injection, cognitive walkthrough).
4. **Debug** interesting failures — especially those that reveal coupling, invariant violations, or observability gaps.
5. **Refactor** for clarity or resilience while attempting to preserve stable interfaces.
6. **Capture** any new heuristics, pain points, or discovered invariants in the heuristics log.

**Heuristic Capture Format (lightweight):**
```
[Cycle N] [Component/Seam]
Observation: <what happened under stress>
Implication: <architectural or governance consequence>
Evidence: <link to failing run, log snippet, or diff>
Confidence: Low | Medium | High
```

**Minimum Viable Stress Gate (required before H3):**
- At least one non-trivial failure mode has been experienced and diagnosed.
- At least one cross-cutting concern (retry, idempotency, observability, compensation, ordering) has been forced to evolve under pressure.
- The team/agent can articulate 5–15 concrete heuristics that did not exist at the start of H0.

**Anti-patterns to avoid:**
- Endless happy-path feature addition without stress.
- Large refactors that destroy modularity.
- Capturing "hypothetical" heuristics that were never stress-tested.

### H3: Governance Layer Synthesis

**Goal:** Transform the accumulated iteration history, failures, and heuristics into a durable, machine- and human-readable governance specification.

**Required Sections (minimum):**

- **Orchestration Specification**
  - Primary coordination model (orchestrator, choreography, hybrid)
  - State machine definitions (with transitions, guards, and compensation)
  - Event contracts (schemas, exactly-once vs at-least-once, ordering guarantees)
  - Saga / workflow boundaries and compensation strategies

- **Architecture Decision Records (ADRs)**
  - Each decision must reference the specific iteration cycle(s) and heuristic(s) that justified it.
  - Include rejected alternatives with real (not hypothetical) reasons they were rejected.

- **Observability Governance**
  - Required signals (metrics, logs, traces, events)
  - Correlation and causation IDs
  - Alertable conditions and their thresholds
  - Distributed tracing requirements
  - "What we wish we had instrumented on day one" retrospective

- **Failure Mode Taxonomy**
  - Categorized by blast radius, detection method, recovery strategy, and human/operator involvement.
  - Must include at least the failures actually experienced in the MVA.

- **Interface Contracts & Invariants**
  - Stable public surfaces (APIs, events, state stores) with justification.
  - Invariants that must hold across any future implementation.

- **Cross-Cutting Constraints**
  - Security, compliance, multi-tenancy, performance, cost — discovered through use, not speculation.

**Exit Criteria:**
- A reviewer (human or strong model) can answer "why is the architecture this shape?" for every major seam by referencing the governance layer.
- The governance layer is sufficiently complete that a competent implementer could produce a production rebuild without re-discovering the same painful lessons.

**Artifact:** `governance/governance-layer.md` (or split into `orchestration.md`, `adrs/`, `observability.md`, etc.)

### H4: Sacrificial Throw & Rebuild Planning

**Goal:** Formally retire the MVA and produce a high-fidelity rebuild plan whose source of truth is the governance layer.

**Ritual (do not skip):**
- Create `mva/DEPRECATED.md` with a clear statement: "This MVA served its purpose as a heuristic discovery vehicle. It is no longer the source of truth. All future work derives from the governance layer."
- Update any issue trackers or memory systems to mark MVA-related work as planning artifacts, not product artifacts.

**Rebuild Plan Contents:**
- Derived *only* from the governance layer (H3), not from the original request or MVA code.
- Structured as implementation units (compatible with `ce-plan` / `blueprint` consumption if desired).
- Explicitly calls out which MVA code paths are being discarded vs re-implemented cleanly.
- Includes verification strategy that re-uses the stress scenarios discovered in H2.

**Exit Criteria:**
- The rebuild plan is actionable by a fresh agent or team who has never seen the MVA.
- The plan is high-confidence because every major risk has already been encountered.

### H5: Rebuild Execution (Still Planning in Spirit)

**Goal:** Execute the rebuild, producing a production-grade system whose architecture is justified by experience rather than foresight.

**Characteristics of a successful H5 rebuild:**
- Dramatically cleaner module boundaries than the MVA.
- Observability and governance concerns addressed from day one, not retrofitted.
- Failure modes have documented, tested recovery paths.
- The system "feels" like it was designed by someone who had already lived through its failure modes.

**Relationship to "Implementation" Tools:**
- H5 can be executed with `ce-work`, Sisyphus workers, or any other execution harness.
- The governance layer replaces the traditional requirements/plan document as the primary input.

## Artifact Inventory

```
heuristics/
├── mva-spec.md                 # H0 output — scope and known debt contract
├── mva/                        # Sacrificial implementation (eventually deleted or archived)
│   ├── SACRIFICIAL.md
│   └── DEPRECATED.md           # Written in H4
├── iteration-log.md            # Running record of H2 cycles and heuristic captures
├── governance/
│   ├── governance-layer.md     # Primary synthesis artifact (H3)
│   ├── adrs/
│   ├── orchestration.md
│   ├── observability.md
│   └── failure-taxonomy.md
├── rebuild-plan.md             # H4 output — high-fidelity plan for production rebuild
└── heuristics-catalog.md       # Curated, high-confidence heuristics for future reference
```

## Integration with ECC Ecosystem

- **bd (beads)**: Create issues for MVA work with `type: planning-heuristic`. Mark governance extraction as a distinct phase.
- **thoughtbox / graph-of-thoughts**: Record major "why" insights as observations during H2. The governance layer can be ingested as a knowledge graph.
- **ce-plan / blueprint**: The H4 rebuild plan can be consumed or transformed into a `ce-plan` document or Blueprint construction plan.
- **Prometheus / `/plan`**: Heuristics can be invoked as a specialized mode when Prometheus detects high architectural uncertainty during interview.
- **Sisyphus**: H5 rebuild execution can be orchestrated by Sisyphus once the governance layer exists.

## Anti-Patterns and Failure Modes

- **Feature Creep in the MVA** — Adding product features that are not required to stress the architecture. The MVA is a probe, not a prototype.
- **Premature Elegance** — Refactoring for beauty before the real stresses have been felt. Elegance is an output of H5, not H1–H2.
- **Heuristic Laundering** — Writing down "we believe X" as if it were discovered through iteration. Every heuristic must have a traceable cycle.
- **Ghost in the Machine** — Keeping useful MVA code "because it works" without re-justifying it against the governance layer. This pollutes the final system with planning artifacts.
- **Insufficient Stress** — Declaring H2 complete after only happy-path evolution. The governance layer will be weak and the rebuild will re-discover the same problems in production.

## Command and Invocation

Once installed, invoke with:

```
/heuristics <one-line objective or reference to requirements>
```

The skill will guide the user through H0 (interview + mva-spec co-creation), then proceed through H1–H5 with explicit phase gates and artifact production.

For lighter-weight or exploratory use, the skill can also be invoked in "governance extraction only" mode on an existing codebase that was built with heuristic intent.

## Installation (Development)

This skill is currently developed in `~/ideas/heuristics`. To use it locally:

```bash
# Symlink or copy into your skills directory
ln -s ~/ideas/heuristics ~/.agents/skills/heuristics
# or
cp -r ~/ideas/heuristics ~/.agents/skills/heuristics
```

After installation, `/heuristics` becomes available.

---

**Status:** This document is the canonical definition of the Heuristics planning methodology. It will evolve as the skill is used on real problems and as the artifact formats, phase gates, and integration patterns are refined through practice.