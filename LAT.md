# LAT

**Living Architecture Trace for the Heuristics Methodology**

This file follows the `lat.md` authoring conventions (strict leading paragraphs, section identity, wiki-style linking).

---

## What This File Is

`LAT.md` is the structured, cumulative knowledge base for the *Heuristics planning methodology itself*.

It records discoveries, refinements, and meta-heuristics that have emerged from real usage across multiple projects. It is the primary document an agent should consult when it needs to understand "how Heuristics is actually practiced" rather than "what the initial spec said."

---

## Reading Order in This Repo

When working on or with the Heuristics project, follow this order:

1. `AGENTS.md` — how to work on *this repo*
2. `LAT.md` + `SKILL.md` — what the methodology has become through use
3. `MVA.md` / `SPEC.md` / `DESIGN.md` — the formal contracts and implementation design
4. `GOAL.md` — the deepest "why"

---

## Core Concepts

### Heuristic

A concrete, evidence-backed observation about architectural discovery that was forced by stress on an MVA.

Every heuristic in this document must eventually trace back to a specific cycle in a real engagement's iteration log.

### Governance Layer Evolution

Changes to what sections, fields, or invariants are considered mandatory in a governance layer after multiple projects.

### Phase Gate Refinement

Modifications to the strictness, ordering, or exit criteria of H0–H5 that were required by lived experience.

---

## Discovered Heuristics

### The Minimum Viable Stress Gate is Load-Bearing

Weak governance layers almost always come from insufficient stress during H2, not from insufficient synthesis skill in H3.

**Evidence:** Multiple early internal runs where teams produced beautiful but hollow governance documents after only happy-path iteration.

**Implication:** The H2 → H3 gate must remain strict even when the user is eager to "move on."

### Psychological Attachment to the MVA is the Primary Failure Mode

Teams and agents frequently fall in love with the MVA they built and begin negotiating "how much of it we can keep."

**Evidence:** Observed in the creation of the methodology itself and in early test runs.

**Implication:** The H4 deprecation ritual (`mva/DEPRECATED.md`) must be performed explicitly and without negotiation.

---

## Governance Layer Schema Changes

### Added "Day One Regret" Retrospective

After the initial methodology creation, we added a required "Day One Regret" section in the observability part of every governance layer.

This forces synthesis to surface instrumentation debt that only became visible under real failure injection.

---

## Phase Gate Adjustments

### H2 Graduation Now Requires Explicit Evidence

Originally H2 graduation was somewhat subjective ("we feel we have learned enough").

It was strengthened to require:
- At least one diagnosed distributed failure
- At least one cross-cutting concern that visibly evolved
- 5–15 traceable heuristics in the iteration log

---

## Open Questions

### How Much of the Governance Layer Can Be Auto-Synthesized?

Early evidence suggests that orchestration contracts and failure taxonomy require strong human judgment, while observability requirements can be partially auto-generated from iteration logs.

This question is still active.

---

## How to Add New Entries

When a real Heuristics engagement produces a significant discovery:

1. Add a new top-level section with a clear, stable heading.
2. Write a leading paragraph (≤250 characters) that gives the section its identity.
3. Include concrete evidence (project, cycle, symptom).
4. State the implication for future runs or for updates to `SPEC.md` / templates.
5. Link back to the source engagement's governance layer or iteration log using `[[ ]]` wiki link style when possible.

---

*This file is intentionally structured for agent navigation and long-term accumulation. It is not a narrative.*