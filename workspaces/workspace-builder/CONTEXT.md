# Workspace builder

Purpose: Scaffold new Boom ICM projects through five structured stages, with automatic packaging/isolation rules.

Inputs: User initiative description, Boom foundation structure

Process: Five stages (discovery → mapping → scaffolding → packaging → questionnaire → validation)

Output: Complete project folder under `projects/[name]/` meeting all 22 conventions

Done-looks-like:
- Project folder exists with stages 01, 02, 03… numbered and named
- `_agent/` folder is populated with definition.md, identity.md, boundary.md, connectors.md, guards.md, invocation.md
- `evals/tasks/` seeded with one task per stage
- All 22 conventions pass validation
- Human approved definition.md, identity.md, boundary.md

Failure modes:
- User unsure how many stages needed (mitigated: default to 3, add more in questionnaire)
- Workspace is personal scratch but builder enforces packaging (mitigated: ask exemption question, write EXEMPT.md if yes)
- Stage CONTEXT.md left with placeholders (mitigated: validation checks, refuse to finish if any placeholders remain)

## Stages

**01-discovery:** Gather intent, owner, timeline, data scope  
**02-mapping:** Identify stages, systems, touchpoints, write access  
**03-scaffolding:** Create folder structure (automated)  
**03b-packaging:** Scaffold `_agent/` folder (automated)  
**04-questionnaire:** Fill per-stage details  
**05-validation:** Verify all conventions (automated)

Human review checkpoints after stages 02, 03b, 04, 05.
