# Boom ICM Foundation

Complete ICM (Interpretable Context Methodology) structure with Packaging Layer, ready to use.

## What's in this repo

- **CLAUDE.md** — Layer 0 routing table (loaded by Claude Code)
- **_core/** — Conventions, packaging spec, voice, format guidelines
- **workspaces/workspace-builder/** — Agent for scaffolding new projects
- **projects/** — Your project folders (one per initiative)
- **plugins/boom-icm-foundation/** — The `/boom:workspace-builder` skill, shipped as a plugin
- **.claude-plugin/marketplace.json** — Makes this repo an installable Claude Code marketplace
- **team/** — Team account rollout: enforced settings, admin runbook, member how-to

## Quick start

### New device
1. Clone this repo
2. Claude Code reads CLAUDE.md automatically
3. Run `/boom:workspace-builder` to start a project

### New project
```
/boom:workspace-builder [project name]
```

### Read first
- **START_HERE.md** — Entry point
- **WORKSPACE_BUILDER_README.md** — When to use the builder
- **BOOM_ICM_COMPLETE_WITH_PACKAGING.md** — Full spec

## The rules

Read `_core/CONVENTIONS.md` for all 22 conventions. Key ones:

1. Docs over outputs (read CONTEXT.md, not stage outputs)
2. Stage contracts explicit (Purpose/Inputs/Process/Output/Done-looks-like/Failure-modes)
3. Stages work in order (01 → 02 → 03…)
4. Human review between stages
5. Packaging (`_agent/`) required for non-personal-scratch workspaces

## For your team

- Push to GitHub
- Team members clone
- Layer 0 CLAUDE.md loads automatically
- Run `/boom:workspace-builder` to scaffold new projects

## Support

- See `_core/PACKAGING.md` for isolation rules
- See `workspaces/workspace-builder/CONTEXT.md` for the five-stage process
- See `_references/` for external links (never copies internal)

---

**Version:** 2.0 (Boom ICM 1.0 + Packaging Layer 1.0)  
**Author:** Timber (timber@boominteractive.io)

## Team account

The whole team gets this method and the `/boom:workspace-builder` skill through the Claude Team account — nobody installs anything by hand.

- **Admins:** `team/TEAM-SETUP.md` — deploy `team/managed-settings.json` once.
- **Everyone else:** `team/HOW-TO-USE.md` — how to use the skill.

Enforcement is two-sided: managed settings inject the rules and the skill into every session, and `boom-icm-check` CI blocks a merge when a repo or project doesn't conform.
