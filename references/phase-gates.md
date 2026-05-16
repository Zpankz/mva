# Heuristics Phase Gates — Entry, Exit, and Anti-Patterns

This reference defines the formal gates between H0–H5. These are not bureaucratic checkboxes; they are **quality and epistemological boundaries**. Crossing a gate without meeting the criteria produces a weak governance layer and defeats the purpose of the methodology.

---

## H0 Gate: MVA Specification Agreed

**Entry Trigger:** User invokes `/heuristics` with a problem that has architectural uncertainty.

**Exit Criteria (all must be true):**

- [ ] The 3–7 core architectural seams/uncertainties are explicitly named and ranked by risk.
- [ ] The MVA scope is small enough that a competent implementer could build a runnable version in hours to a few days (not weeks).
- [ ] The "Known Technical Debt & Simplifications" list is explicit, non-controversial, and includes persistence, error handling, security, observability, and deployment dimensions.
- [ ] Module boundaries and primary contracts are named at a level that allows independent evolution.
- [ ] Minimum Viable Stress criteria are written and measurable.
- [ ] The user (or stakeholder) has explicitly said "yes, this scope is sufficient to discover what we need to know" — not just "looks good."

**Anti-Patterns That Invalidate the Gate:**

- MVA scope is actually the full product ("we'll just build the real thing and call it an MVA").
- Known debt list is vague ("we'll simplify auth") without saying *how* it is simplified.
- No Minimum Viable Stress criteria defined (the gate becomes "we feel like we're done iterating").

**Output Artifact:** `heuristics/mva-spec.md` (agreed status)

---

## H1 Gate: MVA Is Runnable

**Entry Trigger:** H0 gate passed + user says "build the MVA" or "proceed to H1."

**Exit Criteria:**

- [ ] The primary happy path(s) defined in the mva-spec execute end-to-end without crashing.
- [ ] Module boundaries are clear enough that an agent unfamiliar with the code can identify "which files belong to which module" with >90% accuracy.
- [ ] The entire `mva/` directory (or equivalent) is marked as sacrificial (`SACRIFICIAL.md` or per-file markers).
- [ ] Basic instrumentation exists to observe the behavior of the seams under test (logs, simple metrics, or trace output).

**Anti-Patterns:**

- Building additional product features "while we're here" that were not required to stress the architecture.
- Optimizing or polishing the MVA (premature elegance).
- Skipping the sacrificial marking ritual.

**Output:** Working MVA + iteration log initialized.

---

## H2 Gate: Minimum Viable Stress Achieved (Most Important Gate)

**Entry Trigger:** H1 complete + agent begins deliberate iteration under stress.

**Exit Criteria (non-negotiable):**

- [ ] At least one **non-trivial distributed or cross-module failure** has been experienced, diagnosed, and (partially or fully) mitigated through iteration.
- [ ] At least one **cross-cutting concern** (retry/idempotency, compensation, ordering, observability, rate limiting, multi-tenancy, etc.) has been forced to evolve under pressure, revealing coupling that was not visible in H0/H1.
- [ ] The iteration log contains **5–15 concrete heuristics** with traceable evidence from specific cycles.
- [ ] The team/agent can articulate, in plain language, "the architecture has shown us its true shape" — and can point to the specific failures and refactors that produced that conviction.
- [ ] Module boundaries have been pressure-tested (some may have been changed or justified as stable).

**Anti-Patterns That Must Block Graduation:**

- Only happy-path evolution for many cycles.
- "We added more features to the MVA" instead of stressing the existing seams.
- Heuristics are written as hypotheses ("we believe X will be important") rather than as post-experience statements ("after cycle 7, we learned that...").
- The agent is reluctant to inject failure or load because "it might break things" — breaking things is the point.

**Evidence the Gate Is Weak (Even If Checkboxes Are Checked):**

- All heuristics are about local module behavior; none are about orchestration, state boundaries, or cross-cutting governance.
- The failure that was "diagnosed" was actually just a bug fix, not an architectural revelation.
- The team cannot tell you which invariants are now known to be load-bearing.

**Output:** Iteration log + heuristics catalog (draft) + strong conviction that H3 synthesis will be high-value.

---

## H3 Gate: Governance Layer Is Traceable and Sufficient

**Entry Trigger:** H2 gate passed + user says "synthesize the governance layer."

**Exit Criteria:**

- [ ] Every major section of the governance layer (orchestration, ADRs, observability, failure taxonomy, invariants) is backed by at least one heuristic or specific cycle in the iteration log.
- [ ] A reviewer (human or strong model) can answer "why is it this shape?" for the top 3–5 architectural decisions by pointing to concrete evidence, not speculation.
- [ ] The "Day One Regret" retrospective in observability is non-empty and specific.
- [ ] The failure mode taxonomy includes real (not hypothetical) modes experienced in the MVA.
- [ ] Open questions and known weaknesses are explicitly called out with "minimum additional stress required to resolve."

**Anti-Patterns:**

- Copying MVA implementation details into the governance layer as if they were the desired end state.
- Writing beautiful but untraceable prose ("the orchestrator should be idempotent") without linking to the cycle that proved why.
- Treating the governance layer as a requirements document rather than a post-experience synthesis.

**Output Artifact:** `governance/governance-layer.md` (synthesized or ratified status)

---

## H4 Gate: MVA Is Formally Deprecated + Rebuild Plan Exists

**Entry Trigger:** H3 complete.

**Exit Criteria:**

- [ ] `mva/DEPRECATED.md` (or equivalent) has been written with a clear statement that the MVA is no longer the source of truth.
- [ ] The rebuild plan (`rebuild-plan.md`) derives *exclusively* from the governance layer. Any reference back to the original user request or MVA code is only for historical context, not as a specification input.
- [ ] The rebuild plan is structured so that a fresh agent (who has never seen the MVA) can execute it with high confidence.
- [ ] The "throwaway ritual" has been performed and acknowledged by the user.

**Anti-Patterns:**

- "This MVA code is actually pretty good, let's just clean it up instead of rebuilding" — this is the most dangerous and common failure mode.
- Rebuild plan still contains "we should do X because the MVA did Y" without re-deriving X from the governance layer.

**Output:** Deprecated MVA + high-fidelity rebuild plan.

---

## H5 Gate: Rebuild Complete and Governance Layer Honored

**Entry Trigger:** H4 complete + user decides to execute the rebuild (still under the Heuristics planning umbrella).

**Exit Criteria:**

- [ ] The production system passes all verification scenarios defined in the rebuild plan.
- [ ] The governance layer (or a living version of it) has been carried forward into the production codebase (ADRs in repo, observability contracts enforced in code, orchestration engine matching the spec, etc.).
- [ ] No "ghost code" from the MVA has survived without explicit re-justification against the governance layer.
- [ ] The team can articulate the difference in confidence between "this architecture was planned" vs "this architecture was discovered through stress and then planned."

**Anti-Patterns:**

- Treating H5 as "normal implementation work" and forgetting the governance layer.
- Allowing MVA patterns to leak in "because they worked."

---

## Meta-Gate: When to Abort or Pivot

At any point, the user or agent may decide that the Heuristics process is not adding value. Acceptable pivot points:

- After H0, if the architectural uncertainties turn out to be less severe than feared → pivot to `ce-plan` or `blueprint`.
- During H2, if the MVA is revealing only local bugs and no cross-cutting architectural pain → consider whether a simpler planning approach would have sufficed.
- After H3, if the governance layer is thin despite real stress → the methodology exposed its own limits for this problem class; document the meta-heuristic.

In all cases, the decision to abort should be recorded with the reason. This is valuable data for the evolution of the framework.

---

**This document is part of the skill.** When in doubt about whether a gate has been met, re-read the anti-patterns. The spirit of the gate is more important than the letter of the checklist.