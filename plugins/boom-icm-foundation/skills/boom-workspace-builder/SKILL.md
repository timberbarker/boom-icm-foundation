---
name: boom-workspace-builder
description: Scaffold a new Boom project as an ICM workspace with the Packaging Layer. Use at the START of any new Boom initiative, or when the user says "new project", "scaffold a workspace", "set up a project folder", "/boom-workspace-builder", or asks how to structure work so Claude can run it. Walks discovery → mapping → scaffolding → packaging (_agent/) → stage contracts → validation, and refuses to finish until all 22 ICM conventions pass. Also use when a shared, scheduled, or client-facing workspace is missing its _agent/ folder.
---

# Boom workspace builder

Scaffolds `projects/<name>/` as a complete ICM workspace. Six stages, four human checkpoints, hard validation at the end.

Method reference: `references/conventions.md` (the 22 rules) and `references/packaging.md` (the `_agent/` spec and templates). Read the relevant one before writing files — do not invent templates.

## Before you start

Confirm three things. Ask if unclear.

1. **Repo** — you are in the `boom-icm-foundation` repo (or a repo scaffolded from it). If there is no root `CLAUDE.md` with a routing table, stop and say so.
2. **Name** — a kebab-case project slug. Derive it from the initiative, confirm it with the user.
3. **Exemption** — is this personal scratch? Personal scratch = one author AND personal data AND manual invocation only. If any one of those is false, it is **not** exempt and it gets `_agent/`.

Never scaffold stages before `_agent/definition.md` exists (except for an exempt workspace).

## Stage 01 — Discovery

Ask, in one message, and wait:

- Who owns this? Who else runs it?
- What does it produce? One sentence.
- Why now — what breaks if it doesn't exist?
- By when?
- Whose data does it touch? Internal, a named client, or a tenant?

Write nothing yet. If answers are thin, ask once more rather than guessing.

## Stage 02 — Mapping — CHECKPOINT

Ask:

- What are the stages, in order? Default to three (discovery → execution → handoff) if the user is unsure; more can be added in Stage 04.
- What systems does it touch (APIs, MCP servers, drives, dashboards)?
- Which stage writes, and where?
- How does a run start — a human typing, a schedule, a webhook, a dashboard action?

Present the proposed stage list and system list back. **Stop for approval before scaffolding.**

## Stage 03 — Scaffolding (automated)

Create, using the numbering the user approved:

```
projects/<name>/
  CONTEXT.md
  stages/
    01-<slug>/CONTEXT.md
    01-<slug>/output/.gitkeep
    02-<slug>/CONTEXT.md
    02-<slug>/output/.gitkeep
    ...
  evals/tasks/.gitkeep
  evals/RESULTS.md
  memory/durable/.gitkeep
```

Every `CONTEXT.md` uses the six-field contract: Purpose / Inputs / Process / Output / Done-looks-like / Failure modes. Copy the shape from `projects/example-project/`. Keep every file under eighty lines.

## Stage 03b — Packaging — CHECKPOINT

If exempt: write `projects/<name>/_agent/EXEMPT.md` stating which of the three scratch tests it passes, the owner, and a review date. Skip to Stage 04.

Otherwise create all six files from the templates in `references/packaging.md`:

```
_agent/definition.md    model, owner, status, tenant, what's attached
_agent/identity.md      whose data, credential source, cross-tenant stance
_agent/boundary.md      may read / may write / may execute / never
_agent/connectors.md    one row per remote surface, include-lists only
_agent/guards.md        ordered: redact → log → meter → approve → retry
_agent/invocation.md    every path a run can start from
```

Fill them from the Stage 01–02 answers. Leave no placeholder text. `definition.md` must name a model.

**Stop.** Tell the user to read `definition.md`, `identity.md`, and `boundary.md` before anything runs. These three are the ones that cause real damage when wrong.

## Stage 04 — Questionnaire — CHECKPOINT

Walk the stages one at a time and fill each `CONTEXT.md`:

- Purpose — one sentence, what this stage is for
- Inputs — named files or upstream stage outputs, explicitly
- Process — the steps
- Output — what lands in `output/`, in what format
- Done-looks-like — unambiguous, checkable
- Failure modes — what goes wrong, and the mitigation for each

Seed `evals/tasks/<stage>.md` with one task per stage, using the template in `references/packaging.md`. Present the filled contracts and **stop for approval**.

## Stage 05 — Validation (automated) — CHECKPOINT

Check every convention in `references/conventions.md` and report a pass/fail line for each. Hard failures — do not report success while any of these hold:

- Any placeholder text (`[name]`, `TODO`, `[person]`) remains anywhere in the tree
- Any file exceeds eighty lines
- Any `CONTEXT.md` is missing one of the six fields
- `_agent/` is absent and there is no `EXEMPT.md` justifying it
- `definition.md` names no model
- `invocation.md` omits a trigger the user described in Stage 02
- A stage writes outside the tree and `boundary.md` does not permit it
- A connector is used that `connectors.md` does not list

Fix what you can, then re-run the check. List anything you cannot fix and say plainly that validation failed.

## Finishing

1. Add the project to the **Project map** table in the root `CLAUDE.md`.
2. Report: path, stage list, exempt or packaged, validation result. One short block.
3. Tell the user to commit. Do not commit or push unless asked.
4. Never self-merge the PR.

## Boundaries

- Write only inside `projects/<name>/`, plus the one Project-map row in root `CLAUDE.md`.
- Do not run project code, connect a server, or reach outside the tree during scaffolding.
- Retrofitting an existing workspace is a different job — follow the retrofit process in `references/packaging.md`, do not run this builder over it.
- Designing an ICM from scratch for a non-Boom process is `icm-architect`, not this.
