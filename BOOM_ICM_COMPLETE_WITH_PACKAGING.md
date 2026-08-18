# Boom ICM Complete with Packaging Layer

**For:** Boom Interactive (all devices, team accounts)  
**Version:** 2.0 (Core ICM 1.0 + Packaging Layer 1.0)  
**Date:** 2026-08-18  
**Author:** Timber (timber@boominteractive.io)  

---

## What this is

One complete file. Everything you need to scaffold a new project or sync a new device:
- Core ICM structure (L0–L4, conventions 1–22)
- Packaging Layer extension
- All templates ready to copy
- Integration checklist

Start here on any new device. One file replaces the bootstrap process.

---

## TL;DR — Five minutes

```bash
# On a new device:
# 1. Create your project directory
mkdir my-project && cd my-project

# 2. Create the folder structure (copy from Part 3 below)
# 3. Copy the CLAUDE.md template (Part 4)
# 4. Copy CONVENTIONS.md (Part 5)
# 5. Copy PACKAGING.md (Part 6)
# 6. Copy workspace builder (Part 7)
# 7. Commit

git init
git add .
git commit -m "init: Boom ICM with Packaging Layer"
```

**Next session:** Claude Code reads Layer 0 `CLAUDE.md`, enforces the rules.

---

## Part 1. Why this file exists

On a new device, you need:
- The ICM folder structure (L0–L4)
- Layer 0 `CLAUDE.md` with all rules
- `_core/CONVENTIONS.md` (1–22)
- `_core/PACKAGING.md` (the spec)
- Workspace builder scaffolding

Pulling from `boom-project-foundation` works, but this file gives you everything inline, synced to today's date, ready to copy-paste.

Use this for:
- **New devices** — Clone your project repo, you're done
- **New team members** — Share this file, they bootstrap in minutes
- **Starting a new project** — Copy the templates, answer the questions
- **Retrofitting existing projects** — Use Part 3 sections to fill gaps

---

## Part 2. The folder structure

Copy this exactly. It's your L0–L4 hierarchy.

```
my-project/
  CLAUDE.md                    ← Layer 0: routing table (see Part 4)
  README.md                    ← Layer 0: what this project is
  
  _core/
    CONVENTIONS.md             ← 22 conventions (see Part 5)
    PACKAGING.md               ← Packaging spec (see Part 6)
    VOICE.md                   ← L3: voice and tone (see Part 3b)
    CONSTRAINTS.md             ← L3: build constraints
    FORMAT.md                  ← L3: output format patterns
  
  workspaces/
    workspace-builder/         ← Scaffolding agent (see Part 7)
      CONTEXT.md
      stages/
        01-discovery/
        02-mapping/
        03-scaffolding/
        03b-packaging/
        04-questionnaire/
        05-validation/
  
  _references/                 ← L3: anything read-only (links, not copies)
    FOUNDATION.md              ← Point to ~/boom-project-foundation/FOUNDATION.md
    BRAND.md                   ← Point to brand kit
  
  projects/
    project-name/              ← L1/L2: one per active project
      CONTEXT.md               ← Stage contract: Purpose/Inputs/Process/Output
      stages/
        01-phase-name/
          CONTEXT.md
          output/
        02-phase-name/
          CONTEXT.md
          output/
      _agent/                  ← L3: packaging (auto-scaffolded, see Part 6)
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
        .gitkeep
```

**Rules:**
- One folder per active project (L1/L2)
- One folder per stage inside the project
- `_core/` is read-only config, referenced by all projects
- `workspaces/` contains the agents that scaffold new projects
- `_references/` points outward (never copies)

---

## Part 3. L3 Config files (copy these)

### Part 3a. `_core/VOICE.md`

```markdown
# Voice and tone

## Boom Interactive
US English always. Plain, direct, product-driven.

- No filler. No hedging. Recommend a path; don't survey options.
- Keep it short. Simple words. One idea per sentence.
- Don't recap work in detail — one-line result is enough unless asked.
- Product-driven: solve the problem, don't describe the problem.

## For this project
[Add project-specific voice guidelines if different]

## Do not
- Apologize or hedge
- Offer multiple options when you can recommend
- Use filler words (actually, basically, clearly)
- Recap what you just did
```

### Part 3b. `_core/CONSTRAINTS.md`

```markdown
# Build constraints

## Scope
[What is in scope for this project]

## Not in scope
[Explicit denials]

## Data policy
[What data this project touches, where it lives]

## Time zone
[Recurring tasks and scheduling defaults to this zone: US/Eastern]

## Tools
[Preferred tools, integrations, blocked tools]

## Quality gates
[What must be true before handoff: tests, reviews, approvals]
```

### Part 3c. `_core/FORMAT.md`

```markdown
# Output format patterns

## Prose
Short paragraphs. One idea per paragraph. No more than two sentences.

## Code
- Inline code examples: three lines max (or a file reference)
- Blocks: show input/output side-by-side when possible
- Never more than 10 lines without breaking it up

## Checklists
Use for steps. Never nest more than two levels.

## Tables
Use for comparisons. Keep to 4–5 columns, 5–8 rows.

## File structure
Use tree format, 2-space indent, no trailing slashes.

## Diffs
Show before/after. Highlight what changed.

## Not used
- Multi-page docs (split into smaller files)
- Nested folder trees (show the layers you touched)
- Story format for technical work
```

---

## Part 4. Layer 0 `CLAUDE.md`

Copy this **exactly** into your project root. This is your routing table and enforcement.

```markdown
# [Project Name] — CLAUDE.md (Layer 0)

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

[Add one row per active project once you start work]

| Project | What | Status |
|---------|------|--------|
| | | |

## Next steps

1. Read `_core/CONVENTIONS.md` for the full rule set
2. Read your first workspace `CONTEXT.md` to understand the stage contract
3. Start work in the first stage's folder
```

---

## Part 5. `_core/CONVENTIONS.md`

Copy this into `_core/CONVENTIONS.md`. These are your 22 binding rules.

```markdown
# Conventions

The ICM method rests on 22 explicit conventions. Every workspace follows all 22. Read from top.

## Context (L1/L2/L3)

**1. One way references.** Never copy external content into the repo. Point to it instead. Link always; embed never (except for brand assets in _references/).

**2. Docs over outputs.** Read the CONTEXT.md file to understand a stage, never the stage's output. Stage outputs are disposable; context is canonical.

**3. Files under eighty lines.** CONTEXT.md and all L3 config: eighty lines max for scanning. Over eighty lines: split into multiple files. REFERENCES (read-only) can be two hundred lines.

**4. Canonical sources.** Each fact lives in one place. No duplication. Link elsewhere. Example: project status lives in one CONTEXT.md, never repeated in other files.

**5. Stage contracts.** Every stage CONTEXT.md names: Purpose · Inputs · Process · Output · Done-looks-like · Failure modes. Nothing is inferred.

**6. Human review between stages.** No stage output is final until a human has reviewed it. Automation between stages is allowed; review is mandatory.

## Execution (L1/L2)

**7. Stages work in order.** Stage 02 does not start until stage 01 output is reviewed. No out-of-order execution.

**8. Each stage has an output folder.** `[stage]/output/` is where final deliverables land. Never write to parent directories.

**9. Workspace routing.** One workspace per active initiative. Inside it: one folder per stage. Stages are numbered and named. Example: `01-discovery/`, `02-mapping/`, `03-scaffolding/`.

**10. Inputs are explicit.** A stage's Inputs section names every file it reads, inside and outside its tree. No surprises.

## Agents and automation (L0/L3)

**11. Bootstrap at the start.** When starting a new project with no conforming root `CLAUDE.md`, scaffold the ICM structure automatically using the workspace-builder or this template. Do not ask the user first.

**12. One model declaration.** Layer 0 `CLAUDE.md` (or workspace `definition.md`) names the model. Nothing else declares a model. Override only in writing.

**13. Voices are stated.** Every project carries `_core/VOICE.md`. Teams inherit it; projects override it. Never infer tone.

**14. Quality gates are explicit.** `_core/CONSTRAINTS.md` names what must be true before handoff (tests pass, reviews complete, approvals granted). Never infer.

**15. Failures become tasks.** Every production failure becomes a checked-in task in `evals/` with one unambiguous pass condition. Fixing the failure without adding the task is incomplete.

## Packaging (L3, added in Packaging Layer)

**16. Agent declaration.** Every non-exempt workspace has `_agent/definition.md`. It is the single canonical answer to "what is this thing, what model runs it, what is attached." See `_core/PACKAGING.md`.

**17. Explicit guard order.** Cross-cutting behavior is listed in order in `_agent/guards.md`. Order is never inferred. Redaction runs before logging, always.

**18. Boundary before execution.** No workspace may execute agent-written code, run shell commands, or write outside its own tree until `_agent/boundary.md` exists and names the permitted paths.

**19. Tenant isolation by default.** `_agent/identity.md` states whose data the workspace touches. Cross-tenant reads are denied unless the file names the exception and reason.

**20. Invocation enumeration.** Every way a run can start is listed in `_agent/invocation.md`. A run path not on the list is a defect, not a feature.

**21. Failures become evals.** Every production failure becomes a checked-in task in `evals/` with one unambiguous pass condition. Fixing the failure without adding the task is an incomplete fix.

**22. Memory split.** Run state and durable knowledge never share a folder. Layer 4 output is disposable. `memory/durable/` survives runs and is never written by a stage without an explicit instruction.

## Enforcement

- Layer 0 `CLAUDE.md` is loaded and enforced by Claude Code on every session
- Conventions 1–22 are the binding standard; nothing overrides them
- Workspaces that cannot meet a convention file an exception in `_agent/definition.md` with reason and review date
- Retrofit existing projects using the five-stage process in `_core/PACKAGING.md` Part 4
```

---

## Part 6. `_core/PACKAGING.md`

This is the full spec for workspaces that leave your hands. Copy this into `_core/PACKAGING.md`.

```markdown
# ICM Packaging Layer

Purpose: ICM covers context. This extends it to cover packaging — capabilities, invocation, isolation and verification. It is an addition to ICM, not a fork. Every existing convention still holds.

## The rule

Every ICM workspace that can be run by anyone other than its author, on any schedule other than a human typing, or against any data other than the author's own, must carry an `_agent/` folder.

Workspaces that fail all three tests are **personal scratch**. They are exempt and should be labelled as such.

## The `_agent/` folder

Seven files. One page each.

### `_agent/definition.md`

# Agent definition

Workspace: [name]
Owner: [person]
Status: dev | pilot | production
Client or tenant: [name, or internal]

## Model
Primary: [provider:model-id]
Fallback: [provider:model-id, or none]
Why this model: [one line]

## Attached
Tools: [list, or none. Points to tools/ entries]
Connectors: [list, or none. Points to _agent/connectors.md]
Guards: [ordered list. Points to _agent/guards.md]
Skills: [list of skills/ entries the stages may load]

## Exempt from
[Any convention this workspace does not meet, with reason and a date to revisit]

### `_agent/connectors.md`

# Connectors

One row per remote surface. No server appears here without an include list.

| Server | Transport | Include only | Used by stage | Auth source |
|---|---|---|---|---|
| corespec | http | [named tools] | 02-spatial | env |

## Denied
[Servers deliberately not connected, and why. Prevents rediscovery]

### `_agent/guards.md`

# Guards

Ordered. Top runs first. Never reorder without noting why.

1. Redact. [What patterns. What replaces them]
2. Log. [What is captured. Where it goes. What is never logged]
3. Meter. [Token accounting, ledger, limits]
4. Approve. [Which actions pause for a human. Who can approve]
5. Retry. [What is retried, how many times, what is never retried]

## Enforcement
[Where each guard is actually enforced today: code, hook, or by hand. Honest answers only]

### `_agent/boundary.md`

# Boundary

## May read
[Paths, inside and outside the workspace]

## May write
[Paths. Default is the workspace tree only]

## May execute
[Commands or none. If none, say none]

## Never
[Explicit denials. Credentials, other tenants, production data, parent directories]

### `_agent/identity.md`

# Identity

Runs as: [single author | named team | per tenant]
Tenant source: [where tenant identity comes from]
Credential source: [where secrets come from. Never the workspace]

## Data scope
This workspace may touch: [tenant data description]
This workspace may not touch: [everything else, stated]

## Cross tenant
Permitted: no | yes, with named exception below
[Exception, reason, approver]

### `_agent/invocation.md`

# Invocation

| Path | Trigger | Who or what | Auth | Rate |
|---|---|---|---|---|
| Interactive | human types in Claude Code | [names] | session | n/a |
| Scheduled | cron [expression] | system | service | [limit] |
| Dashboard | user action | tenant user | tenant token | [limit] |
| Webhook | inbound event | [source] | signed | [limit] |

## Not permitted
[Paths that must not exist. Public unauthenticated invocation, for example]

### `evals/tasks/[slug].md`

# Task: [name]
Origin: [production failure date, or designed]
Stage under test: [stage]
Input: [file or inline]
Pass condition: [one unambiguous statement. Not "output is good"]
Last run: [date, pass or fail]

### `evals/RESULTS.md`

Running table of task, date, result. Nothing more.

## Workspace builder stage: 03b-packaging

When creating a new workspace, stage 03b runs after scaffolding:

**Inputs:** Discovery output (intent/audience), Mapping output (stages/touchpoints), `_core/PACKAGING.md`

**Process:**
1. Run exemption test (three questions: another author? scheduled? other data?)
2. If all no → write `_agent/EXEMPT.md` and stop
3. Scaffold seven files from templates
4. Fill `definition.md` and `identity.md` from discovery
5. Fill `boundary.md` from mapping (what reads/writes outside tree?)
6. Fill `connectors.md` and `invocation.md` from mapping
7. Fill `guards.md` from data sensitivity
8. Seed `evals/tasks/` with one per stage that produces output

**Outputs:** Populated `_agent/`, `evals/` scaffold, `memory/durable/` with `.gitkeep`

**Checkpoint:** Show human `definition.md`, `identity.md`, `boundary.md` before continuing

**Audit:** No placeholders in definition/identity, boundary names explicit denials, every connector has include list, guards are ordered + honest, all files under eighty lines

## Retrofitting existing workspaces

Create `workspaces/packaging-retrofit/` with five stages:

**Stage 01: Inventory** — Walk every workspace. One row per workspace (name, owner, status, who runs it, whose data, writes where, connectors, has evals).

**Stage 02: Triage** — Sort into buckets:
- Bucket A: Client-facing or production (retrofit first, fully)
- Bucket B: Scheduled or unattended (invocation + guards)
- Bucket C: Internal shared (definition + boundary)
- Bucket D: Personal scratch (exempt, never retrofit)

**Stage 03: Scaffold** — Create `_agent/` with seven templates, nothing filled. Separate from populate.

**Stage 04: Populate** — Fill from evidence (model in use, actual data touches, real triggers, grep for writes). Honest answers on enforcement.

**Stage 05: Validate** — Run the validate verb. Report pass/fail per convention. Bucket A failures on 18/19 are stop-line.

**Sequencing:** Stages 01–02 across everything, then Bucket A all the way through 05, then B, then C, then skip D.

## Validation

Claude Code should stop and ask before proceeding if:
- A stage writes outside tree and boundary.md doesn't permit it
- A connector is being added not in connectors.md
- Workspace handed to client and identity.md still says single author
- A schedule is being added and invocation.md doesn't list it
- definition.md names no model

## Done conditions

- `validate` command exists and runs
- Every new workspace created passes on first run
- Every Bucket A workspace passes conventions 16, 18, 19
- `evals/tasks/` is non-empty in Bucket A and B
- One production failure converted to a task and caught by it later
```

---

## Part 7. Workspace builder

Create `workspaces/workspace-builder/CONTEXT.md`:

```markdown
# Workspace builder

Purpose: Scaffold new projects using the ICM method + Packaging Layer

## Stages

01-discovery → 02-mapping → 03-scaffolding → 03b-packaging → 04-questionnaire → 05-validation

## Stage 01: Discovery

**Purpose:** Understand the initiative: who, what, why, by when

**Inputs:** User description, stakeholder list, any existing context

**Process:**
1. Ask for: initiative name, owner, team, client (if any)
2. Ask for: what problem this solves, who benefits
3. Ask for: timeline, success criteria, risks
4. Ask for: what data it touches (internal/client/public)

**Output:** `discovery.md` with answers to above

**Checkpoint:** Human confirms understanding before proceeding

## Stage 02: Mapping

**Purpose:** Identify stages, touchpoints, external systems

**Inputs:** discovery.md

**Process:**
1. List the stages this initiative needs (typically 3–5)
2. Name each stage: what does it produce?
3. Identify what systems/APIs/data stores are touched
4. Identify who has write access to what

**Output:** `mapping.md` with stage list + touchpoint matrix

**Checkpoint:** Human confirms stages and touchpoints

## Stage 03: Scaffolding

**Purpose:** Create the folder structure

**Inputs:** discovery.md, mapping.md

**Process:**
1. Create workspace folder under `projects/[initiative-name]/`
2. Create `CONTEXT.md` template for the workspace
3. Create `stages/01-name/`, `02-name/`, etc.
4. Create `output/` folder in each stage
5. Create `evals/`, `memory/durable/`

**Output:** Folder structure ready to fill

**Checkpoint:** Human reviews structure

## Stage 03b: Packaging

**Purpose:** Define capabilities, isolation, invocation

**Inputs:** discovery.md, mapping.md, scaffolded folders

**Process:**
1. Run exemption test (is this personal scratch?)
2. If not → scaffold `_agent/` with seven templates
3. Fill definition.md, identity.md from discovery
4. Fill boundary.md from mapping
5. Fill connectors.md, invocation.md from mapping
6. Seed evals/tasks/

**Output:** Populated `_agent/`, evals structure

**Checkpoint:** Human reviews definition.md, identity.md, boundary.md

## Stage 04: Questionnaire

**Purpose:** Gather stage-specific details

**Inputs:** Workspace structure + packaging

**Process:**
1. For each stage: ask for inputs, success criteria, failure modes
2. Fill stage CONTEXT.md with Purpose/Inputs/Process/Output/Done-looks-like/Failure-modes
3. Identify review checkpoints between stages

**Output:** Complete CONTEXT.md for each stage

**Checkpoint:** Human confirms stage contracts

## Stage 05: Validation

**Purpose:** Verify the workspace is ready to use

**Inputs:** All outputs from stages 01–04

**Process:**
1. Check all folders exist
2. Check all CONTEXT.md files are populated (no placeholders)
3. Check evals/tasks/ has at least one task per stage
4. Check definition.md, identity.md, boundary.md are filled
5. Run the validate verb against conventions 16–22

**Output:** Pass/fail report

**Done:** All checks pass, workspace ready to use
```

---

## Part 8. Integration checklist

New device? New project? Use this checklist.

- [ ] Create project folder: `mkdir my-project && cd my-project`
- [ ] Create folder structure from Part 2 above
- [ ] Copy Layer 0 `CLAUDE.md` from Part 4
- [ ] Copy `_core/CONVENTIONS.md` from Part 5
- [ ] Copy `_core/PACKAGING.md` from Part 6
- [ ] Copy `_core/VOICE.md`, `_core/CONSTRAINTS.md`, `_core/FORMAT.md` from Part 3
- [ ] Copy workspace builder from Part 7
- [ ] Add project to git: `git init && git add . && git commit -m "init: Boom ICM with Packaging Layer"`
- [ ] On other devices: `git clone` and pull
- [ ] Next Claude Code session: Layer 0 loads, you're ready

---

## Part 9. For your team

### Onboarding new members
1. Share this file
2. They follow Part 8 checklist on their device
3. Next session: they have the rules

### Sharing across team account
1. Commit the structure to your team repo (GitHub, Boom-INC, etc.)
2. Team members pull it
3. Layer 0 `CLAUDE.md` enforces it automatically

### Starting a new project (together)
1. Run `workspaces/workspace-builder` on this machine
2. Follow stages 01–05
3. Commit to your project repo
4. Team members pull and work the stages in order

---

## Part 10. What you have

This one file covers:
- ✓ Core ICM method (L0–L4, conventions 1–15)
- ✓ Packaging Layer (conventions 16–22, `_agent/` folder)
- ✓ Folder templates (copy-paste ready)
- ✓ CLAUDE.md template (Layer 0 routing)
- ✓ CONVENTIONS.md (all 22)
- ✓ PACKAGING.md (full spec)
- ✓ Workspace builder (five stages)
- ✓ Integration checklist

**Use it for:**
- Syncing a new device (Part 8)
- Onboarding new team members (Part 9)
- Starting a new project (run workspace builder)
- Retrofitting existing projects (Part 6 retrofit section)

---

## Questions?

- **Source:** `~/boom-project-foundation/` (canonical foundation)
- **Contact:** Timber (timber@boominteractive.io)
- **Method:** Changes to the foundation cascade to all projects that use this file

---

## Version

**2.0** (2026-08-18) — Core ICM 1.0 + Packaging Layer 1.0, integrated into one shareable file for all devices and team accounts.
