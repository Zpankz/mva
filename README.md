# MVA — The MVA Heuristic Document System

This repository is the canonical home for the **MVA heuristic** — a generative, empirical methodology for architectural discovery on high-uncertainty problems.

The system is built around a small set of `lat.md`-style documents that enforce a disciplined separation between live discovery and stable execution.

## The Core Idea

Instead of "research → write a perfect plan → build once correctly," do:

1. Co-define a small, runnable **Minimally Viable Architecture (MVA)** that stresses the real architectural uncertainties.
2. Implement it (deliberately imperfect).
3. Iterate modularly under real stress (evaluation, debugging, refactoring).
4. Mine **heuristics** — empirical architectural truths — from the pain.
5. Synthesize a **unified governance layer** (orchestration spec + ADRs + observability + failure taxonomy).
6. Explicitly throw the MVA away.
7. Rebuild a high-quality, elegant production system from the governance layer.

The entire process is still the **"plan phase."** The production system is the output of planning, not the start of implementation.

## Philosophy

- **Planning as Generative Heuristic Discovery** — Architecture is not fully knowable through foresight. It must be discovered through lived stress.
- **Sacrificial by Design** — The MVA is planning debt, not technical debt. It must die.
- **Governance Layer as Source of Truth** — The rebuild plan is derived from post-experience synthesis, not from the original request.
- **Minimum Viable Stress** — No governance extraction without real failures and evolved cross-cutting concerns.

## Repository Structure

The repository is deliberately minimal at the root:

- `AGENTS.md` — Primary entry point and meta-instructions for any agent.
- `LAT.md` — Structured knowledge graph and cross-project mappings.
- `SKILL.md` — Adaptive, non-deterministic logic with progressive disclosure.
- `README.md` — This file.
- `resources/` — Detailed explanations of the methodology and lifecycle.
- `templates/` — Production-grade, variable-driven templates for applying the heuristic.

The four working documents used when tackling a new problem (`MVA.md`, `SPEC.md`, `DESIGN.md`, `GOAL.md`) live as clean templates in the `templates/` directory.

## Recommended Reading Order for Agents

```
AGENTS.md
    ↓
LAT.md + SKILL.md
    ↓
resources/ (for deep understanding)
    ↓
templates/ (when starting new work)
```

This order ensures agents first internalize the rules and accumulated knowledge before creating new `MVA.md` journals.

## Project Structure

```
.
├── AGENTS.md                   # Entry point + meta-instructions for the MVA heuristic
├── LAT.md                      # Structured knowledge graph (lat.md style)
├── SKILL.md                    # Adaptive, nuanced logic (progressive disclosure)
├── MVA.md                      # Living journal of iteration (written during discovery)
├── SPEC.md                     # Formal technical specification (post-MVA)
├── DESIGN.md                   # Detailed technical design (post-MVA)
├── GOAL.md                     # Executable contract (synthesized from MVA + SPEC + DESIGN)
├── templates/
│   ├── MVA.md                  # Template for the living journal (lat.md style)
│   ├── SPEC.md                 # Template for the formal spec
│   ├── DESIGN.md               # Template for technical design
│   └── GOAL.md                 # Template for the executable goal
├── README.md
├── commands/
│   └── heuristics.md
└── .grok/skills/heuristics/
    └── SKILL.md
```

## Current Status (May 2026)

- Core philosophy and H0–H5 subphase model defined in `SKILL.md`
- Command, templates, and artifact formats created
- Ready for first real usage on a suitably uncertain architectural problem

## Installation (Local Development)

```bash
# After cloning https://github.com/Zpankz/mva
ln -s ~/path/to/mva ~/.agents/skills/mva
# or
cp -r ~/path/to/mva ~/.agents/skills/mva
```

After installation, `/heuristics <objective>` becomes available in Claude Code.

## When to Reach For This

Use Heuristics when the correct orchestration model, state machine boundaries, observability requirements, or failure handling strategies are genuinely uncertain and the cost of discovering them in production is high.

Do not use for incremental work on well-understood patterns (use `ce-plan` or `blueprint` instead).

## Relationship to Other ECC Planning Tools

| Tool | Epistemology | Primary Output | Best For |
|------|--------------|----------------|----------|
| Prometheus + `/plan` | Speculative | Detailed work plan | Most features |
| `ce-plan` | Rigorous speculative | High-fidelity implementation units + test scenarios | Complex, high-risk features with known domain |
| `blueprint` | Construction planning | Multi-PR dependency graph + cold-start briefs | Large, multi-session projects |
| **Heuristics** | **Empirical / generative** | **Governance layer + rebuild plan** | **High architectural uncertainty, novel orchestration, systems where the "right shape" is only knowable through stress** |

Heuristics can feed into the other tools: the H4 rebuild plan can be consumed or transformed by `ce-plan` / `blueprint`.

## Contributing / Evolution

This methodology will be refined through real use. Every time you run a Heuristics session:

- Note what worked and what was awkward in the phase gates.
- Improve the artifact templates.
- Add new anti-patterns and meta-heuristics.
- Evolve the governance layer schema as new categories of insight emerge.

The goal is not to make this the default planning tool, but to make it the **right** tool for the class of problems where speculative planning is structurally inadequate.

## License / Origin

Developed as part of the author's personal ECC (Everything Claude Code) augmentation layer. Intended for eventual contribution to the broader ECC ecosystem if it proves valuable in practice.

---

**"The only way to discover the limits of the possible is to go beyond them into the impossible — or at least into a deliberately imperfect runnable system that shows you where the real limits are."**