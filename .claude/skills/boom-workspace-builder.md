# boom-workspace-builder

Scaffold a new Boom ICM project through five structured stages.

## When to use

- You're starting a new project and need a checklist
- Your team needs a consistent onboarding for new initiatives
- You want to enforce packaging/isolation decisions upfront
- You're building something shared or scheduled (not personal scratch)

## When NOT to use

- Personal scratch workspace (exempt from packaging)
- Quick throwaway prototype (use `/icm-architect` instead)
- Retrofitting an existing workspace (use the retrofit process in `_core/PACKAGING.md`)

## Invocation

```
/boom-workspace-builder
```

Optional: `/boom-workspace-builder [project name]`

## What it does

Walks through five stages:

1. **Discovery** — Who? What? Why? By when? Whose data?
2. **Mapping** — What stages? What systems? Who writes?
3. **Scaffolding** — Create folder structure (automated)
4. **Packaging** — Define isolation & invocation (automated)
5. **Questionnaire** — Stage contracts & details
6. **Validation** — Verify all 22 conventions pass (automated)

Output: Ready-to-use project folder meeting all conventions.

## Output structure

```
projects/[name]/
  CONTEXT.md
  stages/
    01-[name]/
      CONTEXT.md
      output/
    02-[name]/
      CONTEXT.md
      output/
  _agent/
    definition.md
    identity.md
    boundary.md
    connectors.md
    guards.md
    invocation.md
  evals/
    tasks/
    RESULTS.md
  memory/
    durable/
```

## Checkpoints

Review after: Stage 02 (mapping), Stage 03b (packaging), Stage 04 (questionnaire), Stage 05 (validation).

Critical files to review: `definition.md`, `identity.md`, `boundary.md`.
