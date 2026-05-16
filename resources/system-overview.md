# System Overview

This section provides a high-level view of the MVA heuristic and the document system that supports it.

---

## What the MVA Heuristic Is

The MVA heuristic is a structured approach to architectural discovery for problems with significant uncertainty.

Instead of attempting to specify the correct architecture upfront through speculation, practitioners first build a small, runnable Minimally Viable Architecture while maintaining a living journal of the process.

Only after the MVA has been stressed and validated are the learnings formalized into more permanent technical documentation and an executable goal.

---

## Core Documents

### Root Production Files

These three files form the operational foundation of the methodology:

- `AGENTS.md` — Entry point and meta-instructions for agents working on or with the system.
- `LAT.md` — Structured knowledge graph that maps concepts, symbols, and relationships across projects.
- `SKILL.md` — Contains the adaptive, nuanced logic that guides how the heuristic is applied in different contexts.

### Templates

Located in `templates/`, these are the production-grade, variable-driven templates used when applying the heuristic to a new problem:

- `MVA.md` — The living journal written during active iteration.
- `SPEC.md` — The formal specification derived from a completed MVA.
- `DESIGN.md` — The detailed technical design derived from a completed MVA.
- `GOAL.md` — The executable contract synthesized from MVA + SPEC + DESIGN.

---

## Core Philosophy

High-quality architecture for uncertain systems is best discovered through real, iterative construction rather than pure reasoning.

The temporary nature of the MVA phase is intentional. It protects the final `GOAL.md` from being based on untested assumptions.

All documents follow `lat.md` conventions to maximize long-term agent usability and knowledge retention.

---

*This overview is intentionally concise. Detailed explanations of the lifecycle and usage patterns are available in the sibling documents within this directory.*