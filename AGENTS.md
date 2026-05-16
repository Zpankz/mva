# Agent Instructions — MVA Heuristic

This repository develops the **MVA Heuristic** — a generative, empirical planning methodology centered on the disciplined use of a living `MVA.md` journal.

## Purpose of This Document

`AGENTS.md` serves as the primary entry point and meta-instruction set for any agent working inside this repository. It defines how to behave when developing or applying the MVA heuristic.

## Document Reading Order

When beginning work in this repository, read the core documents in this order:

1. `AGENTS.md` — Understand the rules of engagement and the overall philosophy.
2. `LAT.md` and `SKILL.md` — Absorb the accumulated knowledge and adaptive logic.
3. `MVA.md`, `SPEC.md`, and `DESIGN.md` — Study the current state of the living architecture and its formalized technical expression.
4. `GOAL.md` — Internalize the executable target before taking action.

This order ensures agents encounter validated, post-iteration knowledge before acting on older specifications.

## Core Philosophy

The MVA heuristic replaces speculative, document-first planning with a structured process of building a real, runnable Minimally Viable Architecture, recording the journey in a living journal (`MVA.md`), and only then formalizing the learnings.

Key principles:
- `MVA.md` is written iteratively during active work, not pre-planned.
- `DESIGN.md` and `SPEC.md` are created by decomposing a completed `MVA.md`.
- `GOAL.md` is synthesized from the completed MVA plus its formalized technical documents.
- The MVA is always treated as temporary and is deleted after `GOAL.md` is produced.

## Development Workflow

All meaningful work in this repository follows a consistent rhythm.

New tasks should begin by checking `bd ready` for available work. Claim issues explicitly using `bd update` with status and owner. Major changes to the methodology or documents must be recorded as new cycles in the relevant `MVA.md` or as entries in `LAT.md`.

Before finishing any session, agents must run quality checks, update issue status, execute `bd sync`, perform `git pull --rebase`, push changes, and verify that the repository is up to date with the origin.

## Key Documents and Their Roles

`SKILL.md` contains the adaptive, nuanced instructions that augment how all other documents are interpreted. It is the primary source of non-deterministic logic for the heuristic.

`MVA.md` functions as a living journal. It records what was tried, what succeeded, what failed, and how understanding evolved during the active construction of a working architecture.

`SPEC.md` and `DESIGN.md` represent the formalized technical truth. They are produced only after a `MVA.md` has been completed and validated through real iteration.

`GOAL.md` is the executable contract. It is created from a completed `MVA.md` together with its corresponding `SPEC.md` and `DESIGN.md`, and carries forward both aspiration and hard-won practical learnings.

`LAT.md` serves as the structured knowledge graph. It is maintained after `GOAL.md` exists so that agents executing the goal have reliable, linkable access to symbols, definitions, and relationships.

## Working with Templates

When applying the MVA heuristic to a new problem, begin by copying the appropriate templates from the `templates/` directory. Use `templates/MVA.md` as the primary living document during iteration. Only move to `templates/SPEC.md` and `templates/DESIGN.md` once the MVA journal indicates that a stable architecture has emerged.

All generated documents should follow `lat.md` conventions, including the requirement that every section begins with a leading paragraph that establishes its identity.

## Landing the Plane

Every work session must end with a clean state. This includes updating issues in `bd`, committing all changes, pushing to the remote, and confirming that the repository is up to date with the origin. No session is considered complete until these steps are verified.