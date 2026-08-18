# Boom Foundation — CLAUDE.md (Layer 0)

> This is the project routing table and enforcement layer. Claude Code reads it first on every session.

## Who we are

Boom Interactive — FM / PropTech. Products: CoreSpec 3D (cs3d.ai), FM dashboards, CoreSpec customer portals, investor + company platforms.

## Method — ICM (Interpretable Context Methodology)

All work is structured as an agent-runnable folder: L0 `CLAUDE.md` (routing table) → L1/L2 workspace `CONTEXT.md` (stage contracts) → L3 `_core/` (config) → L4 outputs.

- Read `_core/CONVENTIONS.md` for the 22 rules
- Each workspace/stage has its own `CONTEXT.md` contract (Purpose/Inputs/Process/Output/Done-looks-like/Failure modes)
- Human review between stage handoffs; outputs land in each stage's `output/`
- Stages work in order (01→02→03…)

## Voice

US English always. Plain, direct, product-driven. See `_core/VOICE.md`.

- No filler, no hedging. Recommend a path; don't survey options.
- Keep it short. Simple words. One idea per sentence.
- Don't recap work in detail — one-line result is enough unless asked.

## Rules (do not remove)

- Never self-merge PRs. Open with CI green, hand to the team.
- Every repo must have a conforming root `CLAUDE.md`.
- Ask before writing finished docs to shared drives.
- GitHub is the source of truth; one canonical local folder per project.
- Cite links (Confluence/web URLs), not local file paths, when sharing.
- Don't conflate projects — keep them in separate repos.
- Read the project's `CLAUDE.md` first on every new task.

## Packaging

Non-exempt workspaces carry `_agent/`. See `_core/PACKAGING.md`.

Do not scaffold stages before `_agent/definition.md` exists.

Do not execute, write outside the tree, or connect a server before `boundary.md` and `connectors.md` exist.

## Layers

- **L0** `CLAUDE.md` — routing table (this file)
- **L1/L2** workspace/stage `CONTEXT.md` — stage contracts
- **L3** `_core/` + workspace `_agent/` — config and packaging
- **L4** stage outputs and source material

## Project map

| Project | What | Status |
|---------|------|--------|
| example-project | Boom foundation scaffolding example | active |

## Next steps

1. Read `_core/CONVENTIONS.md` for the full rule set
2. Use `/boom-workspace-builder` to scaffold new projects
3. Work stages in order (01 → 02 → 03…)
