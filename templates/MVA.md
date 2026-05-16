---
lat:
  require-code-mention: false
---

# MVA — {{PROJECT_OR_FEATURE_NAME}}

**Status:** In Progress | Validated | Deprecated  
**Started:** {{DATE}}  
**Last Updated:** {{DATE}}  
**Owner:** {{AGENT_OR_PERSON}}

---

## Purpose

This is the **living journal** of the iterative discovery process used to achieve a real Minimally Viable Architecture (MVA).

It records what was tried, what worked, what failed, key decisions, and evolving understanding — until a working MVA is achieved.

This document is written **dynamically and progressively** during active iteration with the user.

---

## Context & Starting Hypothesis

{{BRIEF_DESCRIPTION_OF_THE_ARCHITECTURAL_PROBLEM}}

Initial hypothesis at the start of iteration:

{{INITIAL_HYPOTHESIS}}

---

## Iteration Log

Each major cycle of work should be recorded as a section below. Use one section per significant iteration or phase.

### Cycle 001 — {{SHORT_TITLE_OR_FOCUS}} — {{DATE}}

**Hypothesis going into this cycle:**

{{WHAT_WE_WERE_TESTING}}

**What was implemented / changed:**

{{BRIEF_DESCRIPTION}}

**What worked:**

- 

**What didn't work / Pain points discovered:**

- 

**Key insight or updated understanding:**

{{INSIGHT}}

**Updated hypothesis / direction:**

{{NEW_DIRECTION}}

**Files / Artifacts touched in this cycle:**

- 

---

### Cycle 002 — {{SHORT_TITLE_OR_FOCUS}} — {{DATE}}

(Repeat the structure above for each iteration)

---

## Current State of the MVA

**What the current working MVA looks like:**

{{DESCRIPTION_OF_CURRENT_ARCHITECTURE}}

**Modules / Components that have stabilized:**

- 

**Remaining areas of uncertainty:**

- 

**Known technical debt accepted in this MVA:**

- 

---

## Decision Log

Major architectural decisions made during iteration (with rationale).

| Decision | Rationale | Date | Status |
|----------|-----------|------|--------|
| {{DECISION}} | {{WHY}} | {{DATE}} | Accepted / Reversed |

---

## Criteria for MVA Completion

This MVA is considered "achieved" when the following are true:

- [ ] The core architectural seams have been stressed and a working shape has emerged.
- [ ] We can clearly articulate what worked and what didn't.
- [ ] The current implementation demonstrates the architecture in action.
- [ ] We have enough validated learnings to decompose into `DESIGN.md` and `SPEC.md`.

**Current assessment against completion criteria:**

{{NOTES}}

---

## Next Steps

{{WHAT_WE_PLAN_TO_DO_NEXT_IN_THE_ITERATION}}

---

*This document follows `lat.md` conventions. Every section has a leading paragraph. New cycles should be added as new `### Cycle N` sections.*