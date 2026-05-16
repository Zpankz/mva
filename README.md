# Heuristics — Generative Planning Through Sacrificial Scaffolding

This repository is the canonical development location for the **Heuristics** planning skill — an inverted, empirical alternative to traditional speculative planning frameworks (Prometheus, `ce-plan`, `blueprint`).

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

## Document Hierarchy (Agent Reading Order)

This repo follows the layered documentation philosophy from:

- [lat.md](https://github.com/1st1/lat.md) (structured, linkable knowledge with strict section rules)
- [goal-forge](https://github.com/michaelpersonal/goal-forge) (SPEC → tightened SPEC → GOAL compilation)
- [DESIGN.md](https://github.com/google-labs-code/design.md) (machine-readable + human rationale)

**Recommended reading order for agents:**

```
AGENTS.md
    ↓
LAT.md + SKILL.md
    ↓
MVA.md / SPEC.md / DESIGN.md
    ↓
GOAL.md
```

### Layer Descriptions

| Layer | Documents | Role |
|-------|-----------|------|
| Entry | `AGENTS.md` | How to work *on this repo* (bd, git, quality gates, landing the plane) |
| Knowledge + Implementation | `LAT.md`, `SKILL.md` | Living trace of the methodology + the executable skill |
| Contracts & Design | `MVA.md`, `SPEC.md`, `DESIGN.md` | What makes a valid MVA, the formal methodology spec, and skill architecture |
| Foundation | `GOAL.md` | Deep "why" and long-term success criteria |

This hierarchy ensures agents encounter the *accumulated practice* (`LAT.md`) before the original *speculation* (`SPEC.md` / `GOAL.md`).

## Project Structure

```
.
├── GOAL.md                     # North star and success criteria
├── SPEC.md                     # Canonical methodology specification (v0.1)
├── DESIGN.md                   # Skill architecture and harness strategy
├── LAT.md                      # Living Architecture Trace (cumulative learnings)
├── SKILL.md                    # Claude Code skill definition
├── README.md
├── AGENTS.md
├── commands/
│   └── heuristics.md
├── templates/                  # Shared artifact templates (mva-spec, governance-layer, etc.)
├── references/
│   └── phase-gates.md
└── .grok/skills/heuristics/
    └── SKILL.md                # Grok-native packed skill (project-scoped)
```

## Current Status (May 2026)

- Core philosophy and H0–H5 subphase model defined in `SKILL.md`
- Command, templates, and artifact formats created
- Ready for first real usage on a suitably uncertain architectural problem

## Installation (Local Development)

```bash
# Symlink into your personal skills directory
ln -s ~/ideas/heuristics ~/.agents/skills/heuristics

# Or copy
cp -r ~/ideas/heuristics ~/.agents/skills/heuristics
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