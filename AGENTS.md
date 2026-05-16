# Agent Instructions — Heuristics Planning Skill

This project develops the **Heuristics** generative planning methodology and its implementation as a first-class skill for both Claude Code (ECC) and Grok environments.

## Quick Reference

```bash
bd ready              # Find available work
bd show <id>          # View issue details (e.g. heur-2io)
bd update <id> --status in_progress
bd close <id>
bd sync
git status
```

## Document Reading Order (for Agents)

When working in this repository, read documents in this order:

1. **AGENTS.md** — How to work on *this repo* (bd, git, quality, landing the plane).
2. **LAT.md + SKILL.md** — The living knowledge graph of the methodology + the skill implementation.
3. **MVA.md / SPEC.md / DESIGN.md** — Formal contracts, methodology rules, and skill architecture.
4. **GOAL.md** — Deepest "why" and success criteria.

This order implements the layered philosophy from `lat.md`, `goal-forge`, and `DESIGN.md` conventions.

## Core Mission

Build and refine an **inverted, empirical planning framework** that:

- Replaces speculative document-first planning with generative discovery through a sacrificial Minimally Viable Architecture (MVA)
- Produces a durable **governance layer** (orchestration + observability + experience-backed ADRs) as the primary planning artifact
- Explicitly throws away the MVA and rebuilds from the governance truths

The methodology is defined in `SKILL.md`. All changes must preserve the philosophical inversion and the strict H0–H5 phase gates (see `references/phase-gates.md`).

## Development Workflow

1. **New work always starts from `bd ready`**
2. Claim an issue with `bd update <id> --status in_progress --owner <your-name>`
3. For Claude Code skill changes: edit `SKILL.md`, templates, references, and the `/heuristics` command in `commands/`.
4. For Grok skill packaging: use `/create-skill` (or the `create-skill` skill) to produce a polished `~/.grok/skills/heuristics/SKILL.md` variant, then sync learnings back to this repo.
5. Test changes by running the skill on real (or simulated) high-uncertainty architectural problems.
6. Capture meta-heuristics about the planning process itself in `heuristics-catalog.md` or new reference docs.
7. Before ending any session: run quality checks, update issues, `bd sync`, `git pull --rebase`, `git push`, verify "up to date with origin".

## Key Files

- `SKILL.md` — Canonical definition of the H0-H5 methodology, when to use, guardrails, and artifact inventory.
- `templates/` — Authoritative templates for mva-spec, governance-layer, iteration-log, heuristics-catalog.
- `references/phase-gates.md` — Formal entry/exit criteria and anti-patterns. Changes here are high-impact.
- `commands/heuristics.md` — The `/heuristics` slash command for Claude Code.
- `README.md` — Positioning relative to `ce-plan`, `blueprint`, Prometheus, etc.

## Issue Tracking (bd)

All tasks, refinements, usage reports, and packaging work are tracked in beads (`bd`).

- Use short, actionable titles.
- Link related issues with `bd dep add <id> --blocks <other-id>` or `--blocked-by`.
- High-priority items: first real usage (heur-2io), Grok skill packaging via create-skill (heur-2cz), ECC marketplace packaging.

## Quality Bar

- Every change to the methodology must be justified by either (a) real usage data or (b) clear first-principles reasoning about why the current gate is insufficient.
- The "Minimum Viable Stress" gate (H2 → H3) and the explicit throw ritual (H4) are sacred — do not weaken them without strong evidence.
- Artifact templates must remain portable and useful to both human planners and agents.

## Landing the Plane (Session Completion)

**MANDATORY before any `git push` or session end:**

1. File any new issues discovered during the work.
2. Run relevant quality checks (markdown lint if available, structure validation, template consistency).
3. Update issue statuses (`bd update ... --status completed` or `in_progress`).
4. `bd sync`
5. `git pull --rebase`
6. `git push`
7. `git status` **MUST** report "up to date with origin/main"
8. Clean up any local `mva/` or runtime artifacts (they are never committed).

Never leave the repo in a dirty state or with unpushed work.

## Integration Points

- Works alongside (does not replace) `ce-plan`, `blueprint`, and Prometheus for different problem classes.
- Produces governance artifacts that can be consumed by `ce-plan` or `blueprint` for the final rebuild execution.
- Compatible with `bd` for tracking MVA work vs governance extraction vs rebuild.
- Future: integration with thoughtbox / graph-of-thoughts for persisting discovered heuristics across sessions.

---

**This project practices what it preaches**: the development of the Heuristics skill itself should eventually be run through a Heuristics planning session once the methodology is mature enough.