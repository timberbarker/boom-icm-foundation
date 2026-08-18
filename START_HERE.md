# Boom ICM + Packaging Layer — Start Here

**For:** New devices, new team members, new projects  
**Time:** 5 minutes to read, 5–15 minutes to scaffold a project  
**Version:** 2.0 (2026-08-18)

---

## What you have

Three complete resources:

| File | What it is | Read when |
|------|-----------|-----------|
| **BOOM_ICM_COMPLETE_WITH_PACKAGING.md** | Everything: folder structure, templates, conventions 1–22, packaging spec, workspace builder | Setting up a new device OR need the full spec |
| **WORKSPACE_BUILDER_README.md** | When to use the `/boom-workspace-builder` skill, what it asks, what you get back | Starting a new project |
| **boom-workspace-builder-skill.md** | The skill itself (copy to `.claude/skills/`) | Installing the skill |

---

## Quick start (you are here)

### New device? (5 min)

1. Read **BOOM_ICM_COMPLETE_WITH_PACKAGING.md** Part 8 (checklist)
2. Copy the folder structure from Part 2
3. Copy Layer 0 `CLAUDE.md` from Part 4
4. Commit and pull on your other devices
5. Next Claude Code session: rules are enforced

### New project? (5–15 min)

1. Read **WORKSPACE_BUILDER_README.md** (when-to-use guide)
2. Run `/boom-workspace-builder [project name]`
3. Answer five questions (discovery + mapping)
4. Get back a complete project folder
5. Commit and start work

### New team member?

1. Share this file + **BOOM_ICM_COMPLETE_WITH_PACKAGING.md**
2. They run the new-device checklist
3. They run the builder for their first project
4. Done

---

## One sentence each

- **ICM (Interpretable Context Methodology):** Folder-based project structure. One routing table (Layer 0 `CLAUDE.md`), one per-stage contract (`CONTEXT.md`), config in `_core/`, outputs in `output/`.
- **Packaging Layer:** Adds `_agent/` folder to projects that aren't personal scratch. Defines isolation, invocation, identity, guards, boundaries.
- **Workspace Builder:** Skill that walks you through five stages (discovery → mapping → scaffolding → packaging → questionnaire → validation) to create a new project folder that meets all 22 conventions.

---

## The rule

**Every project that isn't personal scratch needs an `_agent/` folder.**

Personal scratch = one author, personal data, manual only. If any of those is false, it's not exempt.

The workspace builder enforces this automatically. When you scaffold a new project, it asks: "Is this personal scratch?" If no → it creates `_agent/` with seven files you fill in.

---

## What each file teaches you

### BOOM_ICM_COMPLETE_WITH_PACKAGING.md

- **Part 1:** Why this file exists
- **Part 2:** Folder structure (copy-paste)
- **Part 3:** L3 config templates (VOICE.md, CONSTRAINTS.md, FORMAT.md)
- **Part 4:** Layer 0 CLAUDE.md template (routing table)
- **Part 5:** CONVENTIONS.md (all 22 rules)
- **Part 6:** PACKAGING.md (full spec for `_agent/` folder)
- **Part 7:** Workspace builder CONTEXT.md (five stages)
- **Part 8:** Integration checklist (new devices)
- **Part 9:** Team onboarding
- **Part 10:** Summary

**Read when:** You need the complete picture or you're setting up a new device

### WORKSPACE_BUILDER_README.md

- **When to use / when NOT to use**
- **What it does** (five stages)
- **Comparison table** (builder vs. other tools)
- **What it asks you** (per stage)
- **After the builder finishes** (next steps)
- **Common scenarios** (examples)
- **Troubleshooting**

**Read when:** You're about to start a new project or want to know if the builder is right for you

### boom-workspace-builder-skill.md

- Skill description and invocation
- When to use it
- Output structure
- Step-by-step walkthrough (all five stages)
- Common questions
- Next steps

**Read when:** You're installing the skill or need quick reference

---

## The three files you copy into projects

Inside **BOOM_ICM_COMPLETE_WITH_PACKAGING.md**:

1. **Part 4: Layer 0 CLAUDE.md** → Copy to `your-project/CLAUDE.md`
2. **Part 5: CONVENTIONS.md** → Copy to `your-project/_core/CONVENTIONS.md`
3. **Part 6: PACKAGING.md** → Copy to `your-project/_core/PACKAGING.md`

These three are enough. Everything else (folder structure, workspace builder) you create using the builder or manually.

---

## How it all connects

```
You're starting a new project
         ↓
Use /boom-workspace-builder
         ↓
Builder asks: who, what, why, when, data scope (Stage 01)
Builder asks: what stages, what systems (Stage 02)
Builder creates: folder structure (Stage 03)
Builder creates: _agent/ folder (Stage 03b)
You answer: per-stage details (Stage 04)
Builder validates: all 22 conventions (Stage 05)
         ↓
You get: a complete project folder that's ready to use
         ↓
Commit to git
Work the stages in order (01 → 02 → 03…)
Track failures in evals/tasks/
Refer to _agent/definition.md as source of truth
```

---

## For your team

### Link them to this file
Send this file to your team. It's the entry point.

### They'll want to know:
- When to use the builder (→ WORKSPACE_BUILDER_README.md)
- What the full spec is (→ BOOM_ICM_COMPLETE_WITH_PACKAGING.md)
- How to set up a new device (→ Part 8 of the complete file)

### Show them an example
Run the builder on a small project. Show them the output. Say:
"This is what all our projects look like. Folder structure, stage contracts, packaging rules, failure tracking."

---

## The 22 conventions at a glance

**Context & structure (1–6):**
1. One-way references (point, don't copy)
2. Docs over outputs (read CONTEXT.md, not outputs)
3. Files under eighty lines (keep them scannable)
4. Canonical sources (one fact, one place)
5. Stage contracts (Purpose/Inputs/Process/Output/Done-looks-like/Failure-modes)
6. Human review between stages (checkpoint approval)

**Execution (7–10):**
7. Stages work in order (01→02→03…)
8. Each stage has output folder
9. Workspace routing (one per initiative, stages numbered)
10. Inputs are explicit (named in stage CONTEXT.md)

**Agents & automation (11–15):**
11. Bootstrap automatically (scaffold ICM on new projects)
12. One model declaration (in Layer 0 or definition.md)
13. Voices are stated (in _core/VOICE.md)
14. Quality gates explicit (_core/CONSTRAINTS.md)
15. Failures become tasks (evals/tasks/)

**Packaging (16–22):**
16. Agent declaration (definition.md canonical)
17. Explicit guard order (guards.md, redaction before logging)
18. Boundary before execution (boundary.md exists before running code)
19. Tenant isolation (identity.md names data scope)
20. Invocation enumeration (invocation.md lists every trigger)
21. Failures become evals (same as 15, applies to packaging)
22. Memory split (run state ≠ durable knowledge)

---

## Questions?

**"How do I set up a new device?"**
→ Read BOOM_ICM_COMPLETE_WITH_PACKAGING.md Part 8

**"When should I use the workspace builder?"**
→ Read WORKSPACE_BUILDER_README.md

**"What are all the conventions?"**
→ Read BOOM_ICM_COMPLETE_WITH_PACKAGING.md Part 5

**"How do I retrofit an existing project?"**
→ Read BOOM_ICM_COMPLETE_WITH_PACKAGING.md Part 6 (retrofit section)

**"What does `_agent/` do?"**
→ Read BOOM_ICM_COMPLETE_WITH_PACKAGING.md Part 6 (PACKAGING.md section)

**"How do I install the workspace builder skill?"**
→ Copy boom-workspace-builder-skill.md to `.claude/skills/boom-workspace-builder.md`

---

## Files in this bundle

```
START_HERE.md                              ← You are here
BOOM_ICM_COMPLETE_WITH_PACKAGING.md        ← Everything (specs, templates, conventions)
WORKSPACE_BUILDER_README.md                ← When/how to use the builder skill
boom-workspace-builder-skill.md            ← The skill definition (copy to .claude/skills/)
```

---

## Next steps

1. **Read this file** ✓ (you're doing it)
2. **Read WORKSPACE_BUILDER_README.md** (5 min) if you're starting a project, or
3. **Read BOOM_ICM_COMPLETE_WITH_PACKAGING.md Part 8** if you're setting up a new device
4. **Run `/boom-workspace-builder`** when you're ready to create a project
5. **Commit** and start working

Done.

---

**Version:** 2.0 (2026-08-18)  
**For:** Boom Interactive  
**Author:** Timber (timber@boominteractive.io)
