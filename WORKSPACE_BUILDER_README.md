# Workspace Builder — Complete Guide

**What:** A skill that scaffolds new Boom ICM projects through five structured stages.

**When:** You're starting a new initiative, especially one that's shared, scheduled, or client-facing.

**Invocation:** `/boom:workspace-builder` or `/boom:workspace-builder [project name]`

---

## TL;DR

```
/boom:workspace-builder
```

Answer questions about your initiative. Get back a complete project folder that meets all 22 ICM conventions. Five minutes.

---

## What it does

Creates a project structure in five stages:

```
Stage 01: Discovery    ← You answer: who, what, why, when, whose data
Stage 02: Mapping      ← You answer: what stages, what systems, who writes what
Stage 03: Scaffolding  ← Automated: creates folder structure
Stage 03b: Packaging   ← Automated: creates _agent/ folder (isolation, invocation, identity)
Stage 04: Questionnaire ← You answer: per-stage inputs, success criteria, failure modes
Stage 05: Validation   ← Automated: verifies everything passes conventions 1–22
```

**Output:** A project folder with:
- ✓ Folder structure for 3–5 stages
- ✓ `CONTEXT.md` for workspace + each stage (with Purpose/Inputs/Process/Output/Done-looks-like/Failure-modes)
- ✓ `_agent/` folder (seven files defining isolation, invocation, identity)
- ✓ `evals/tasks/` seeded with one task per stage
- ✓ `memory/durable/` for durable knowledge
- ✓ All conventions 1–22 verified

**Time:** 5–15 minutes depending on how well you know your project.

---

## When to use

### ✓ Use workspace-builder when:

- [ ] Starting a new project (initiative, client delivery, internal platform)
- [ ] Multiple people will run it (shared workspace)
- [ ] It touches client data or internal data (needs isolation)
- [ ] It runs on a schedule or webhook (needs invocation rules)
- [ ] You want a checklist to get it right the first time
- [ ] Your team needs consistency (same structure every time)

### ✗ Don't use workspace-builder when:

- [ ] It's personal scratch (you alone, your data, manual only) — just write `_agent/EXEMPT.md`
- [ ] You're quick-prototyping (use `/icm-architect` instead, much faster)
- [ ] You're retrofitting an existing workspace (use the retrofit process in `_core/PACKAGING.md` Part 4)
- [ ] You already have a project folder and just need to add `_agent/` packaging (manual 10 minutes)

---

## Comparison: Which tool to use?

| Situation | Use this | Why |
|-----------|----------|-----|
| Starting a new project, shared or client-facing | `/boom:workspace-builder` | Enforces packaging upfront; guides you through all decisions |
| Quick prototype, solo, disposable | `/icm-architect` | Faster; no packaging overhead |
| Turning an idea into a structure (general) | `/icm-architect` | More flexible than the builder |
| Existing project needs `_agent/` folder | Manual (10 min) | Just create the seven files; no scaffolding needed |
| Existing project needs full retrofit | Use Part 4 in `_core/PACKAGING.md` | Five-stage retrofit process |

---

## What the builder asks you

### Stage 01: Discovery (you answer these)

- Initiative name
- Owner (single person)
- Team size / names
- Problem it solves
- Success criteria (one line)
- Timeline (weeks/months)
- Client name (if client-facing) or "internal"
- What data it touches (internal / client / public)
- Any known risks

**Output:** `discovery.md` with your answers

### Stage 02: Mapping (you answer these)

- What stages does this initiative need? (typically 3–5)
  - Stage 1 name + what it produces
  - Stage 2 name + what it produces
  - etc.
- What systems/APIs/databases does it touch?
  - For each: what do we read, what do we write?
  - Who has write access?
- Any scheduled triggers (cron, webhooks)?
- Any approval gates between stages?

**Output:** `mapping.md` with your answers

### Stage 03: Scaffolding (automated)

The builder creates:
```
projects/[your-project]/
  CONTEXT.md
  stages/
    01-[stage-1-name]/
      CONTEXT.md
      output/
    02-[stage-2-name]/
      CONTEXT.md
      output/
    [etc.]
  _agent/
  evals/
  memory/
```

### Stage 03b: Packaging (automated)

The builder scaffolds and partially fills:
```
_agent/
  definition.md      ← model, owner, attached tools (filled from discovery)
  identity.md        ← whose data, cross-tenant (filled from discovery)
  boundary.md        ← read/write/execute (filled from mapping)
  connectors.md      ← servers (filled from mapping)
  guards.md          ← template only
  invocation.md      ← triggers (filled from mapping)
evals/
  tasks/[one per stage].md
  RESULTS.md
memory/
  durable/
```

**Checkpoint:** You review `definition.md`, `identity.md`, `boundary.md`. If wrong → builder stops, you fix, it continues.

### Stage 04: Questionnaire (you answer per-stage details)

For each stage:
- What are the inputs? (files, data, API responses)
- What are the outputs? (deliverables)
- What's the success criteria? (one clear statement)
- What are the failure modes? (what can go wrong)
- Who reviews this stage? (checkpoint approval)

**Output:** Complete `CONTEXT.md` for each stage with all these fields filled

### Stage 05: Validation (automated)

The builder verifies:
- [ ] All folders exist
- [ ] All `CONTEXT.md` files have Purpose/Inputs/Process/Output/Done-looks-like/Failure-modes (no placeholders)
- [ ] `evals/tasks/` has at least one task per stage
- [ ] `definition.md`, `identity.md`, `boundary.md` are fully filled (not templates)
- [ ] All 22 conventions pass
- [ ] All files are under line limits (eighty for CONTEXT, two hundred for reference)

**Output:** Pass/fail report. If anything fails, you fix it; builder re-validates.

---

## After the builder finishes

1. **Commit to git**
   ```bash
   git add projects/[your-project]
   git commit -m "init: [project name] via workspace-builder"
   ```

2. **Start work**
   - Read `projects/[your-project]/CONTEXT.md` (workspace routing)
   - Read `projects/[your-project]/stages/01-*/CONTEXT.md` (stage contract)
   - Do the work inside `01-*/` folder

3. **Review between stages**
   - At checkpoint: human reviews stage output
   - If approved: move to next stage
   - If not: iterate on current stage

4. **Track failures**
   - Every production issue → becomes a task in `evals/tasks/[slug].md`
   - Next time you run that stage, the task catches it

5. **Refer to `_agent/definition.md`**
   - This is your source of truth for: model, owner, attached tools, connectors
   - If something changes (new server, new model, new author) → update this file

---

## Common scenarios

### Scenario 1: Start a new client project
```
/boom:workspace-builder Client Name — Platform Name
```
Builder will ask for:
- Client data scope (what can we touch?)
- Approval gates (who reviews before handoff?)
- Schedule (is this webhook-triggered, scheduled, or manual?)
- Output: Full project with client isolation baked in

### Scenario 2: Start an internal dashboard
```
/boom:workspace-builder Internal Analytics Dashboard
```
Builder will ask for:
- Who uses it? (one team or many?)
- What data? (internal only)
- Refresh schedule? (cron trigger?)
- Output: Project with scheduled invocation defined

### Scenario 3: Start a shared research workspace
```
/boom:workspace-builder Research — Competitor Analysis
```
Builder will ask for:
- Team members (who can run this?)
- Data sensitivity (internal, confidential, etc.)
- Output frequency? (weekly, ad hoc?)
- Output: Project with shared authorship + clear failure evals

---

## What each output file does

After the builder finishes, you have:

| File | Purpose | When it matters |
|------|---------|-----------------|
| `CONTEXT.md` (workspace) | Routing table for the project | Every session, before you start work |
| `CONTEXT.md` (each stage) | Contract: what goes in, what comes out, what success looks like | Before and after each stage |
| `_agent/definition.md` | Single source of truth: model, owner, attached tools, connectors | When you want to know "what is this thing" |
| `_agent/identity.md` | Whose data does this touch, can it cross tenants | Before connecting to a new API or system |
| `_agent/boundary.md` | What can we read/write/execute | Before executing agent code or shell commands |
| `_agent/invocation.md` | Every way this can run (manual, scheduled, webhook) | When adding automation or scheduling a run |
| `evals/tasks/[slug].md` | One task per stage, seeded from known failures | When something breaks in production |

---

## Troubleshooting

### "I don't know how many stages I need"
Start with three: discovery, execution, handoff. You can add more during the questionnaire.

### "Can I change things after the builder finishes?"
Yes. All files are yours to edit. If you change data scope or invocation method, update `_agent/identity.md` or `_agent/invocation.md` and document why.

### "Validation failed on convention 18 (boundary before execution)"
You said the workspace reads or writes outside its tree, but `boundary.md` doesn't permit it. Either:
- Add the path to `boundary.md` under "May read" or "May write", or
- Stop reading/writing outside the tree

### "Can I use the builder for a tiny project?"
Yes, but it's overkill for personal scratch (you alone, your data, manual only). For that: write `_agent/EXEMPT.md` and move on. No builder needed.

### "What if I change my mind about the project structure?"
Stop after Stage 02 (mapping). If mapping is wrong, you can scrap and restart the builder. After Stage 03 (scaffolding), changes are local edits, not a full restart.

---

## Integration

This skill is part of your Boom foundation. It lives in:
- **As a skill:** `plugins/boom/skills/workspace-builder/SKILL.md`, delivered to the whole team through the Claude Team account (see `team/HOW-TO-USE.md`)
- **As a workspace:** `workspaces/workspace-builder/` (manual fallback if the skill is unavailable)

If the skill doesn't load, you can still run the builder manually:
```bash
cd workspaces/workspace-builder
# Claude Code reads CONTEXT.md and walks you through the stages
```

---

## For your team

### Tell them to use this skill when:
- Starting a new project together
- Setting up a client delivery
- Building a scheduled/automated workspace
- They want a checklist to avoid mistakes

### Link them to:
- This README (when-to-use guide)
- `BOOM_ICM_COMPLETE_WITH_PACKAGING.md` (full spec, including the builder CONTEXT.md)
- `_core/PACKAGING.md` (detailed packaging rules)

### Show them the output:
- Run the builder on a small example project
- Show them the resulting folder structure + `_agent/` folder
- Explain: "This is what all our projects look like"

---

## Version

**1.0** (2026-08-18) — Boom workspace-builder skill, integrated with core ICM + Packaging Layer.
