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
