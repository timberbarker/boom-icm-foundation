# How to use `/boom:workspace-builder`

For everyone on the Boom Claude Team account. Read once, five minutes.

## You install nothing

The skill and Boom's rules arrive through the Team account. Open Claude Code and they are there. If your first session asks you to approve org settings, approve it — that is the Boom foundation loading.

Check it worked:

```bash
/plugin
```

`boom` should be listed as enabled.

## What you get automatically

Every session, Claude already knows: the ICM method, the six-field stage contract, the Packaging Layer rule, the 60/30/10 triage, Boom's voice, and never self-merge a PR. You do not have to repeat any of it.

If you open Claude in a repo with no conforming root `CLAUDE.md`, you get a `[boom-icm]` warning. That repo is not set up yet — scaffold it before doing real work in it.

## Use it whenever you start a project

```bash
/boom:workspace-builder
```

Or name it up front:

```bash
/boom:workspace-builder savills-fm-pilot
```

Run it from the `boom-icm-foundation` repo, or any repo scaffolded from it. It creates `projects/<name>/`.

## What it asks you

**Discovery.** Who owns this, who else runs it, what it produces, why now, by when, and whose data it touches.

**Mapping.** What the stages are in order, what systems it touches, which stage writes, and how a run starts — a person typing, a schedule, a webhook, a dashboard.

Answer honestly and briefly. If you don't know the stage count, say so — it defaults to three and you can add more later.

## Four places it stops for you

It will not run start to finish on its own. It pauses and waits at:

1. **After mapping** — approve the stage list before anything is written.
2. **After packaging** — read `_agent/definition.md`, `identity.md`, and `boundary.md`. These three decide what the workspace is allowed to touch. Read them properly; this is the checkpoint that matters.
3. **After the stage contracts** — check each stage's Purpose, Inputs, Output, and Done-looks-like.
4. **After validation** — confirm the pass/fail report.

## What you get back

```
projects/<name>/
  CONTEXT.md              what this project is
  stages/01-…/CONTEXT.md  the contract for each stage
  stages/01-…/output/     where that stage's work lands
  _agent/                 six files: what it may touch and how it starts
  evals/tasks/            one task per stage; failures get logged here
  memory/durable/         knowledge that survives a run
```

Then: commit it, work the stages in order, review between stages, open a PR, and hand it to someone else to merge.

## The packaging rule, in one line

If anyone but you can run it, or anything but a person can start it, or it touches data that isn't yours — it needs `_agent/`.

Only personal scratch is exempt, and exempt means all three of those are false. The builder asks, and writes `_agent/EXEMPT.md` if you qualify.

## When not to use it

| Situation | Use instead |
|-----------|-------------|
| Retrofitting an existing project folder | The retrofit process in `_core/PACKAGING.md` |
| Structuring something that isn't a Boom project | `/icm-architect` |
| Throwaway prototype you'll delete today | Nothing — just work |

## If something's off

**The skill isn't listed.** Restart Claude Code. Still missing — check `/plugin`, then ask the admin whether managed settings are deployed.

**It stopped mid-run and asked a question.** That's a checkpoint, not a failure. Answer it.

**Validation failed.** It tells you which convention broke. Usually placeholder text left in a `CONTEXT.md`, or `definition.md` with no model named. Fix and ask it to re-validate.

**It won't scaffold stages.** `_agent/definition.md` has to exist first. That's deliberate.

**CI failed on your PR.** `boom-icm-check` blocks a repo with a broken root `CLAUDE.md` or a project missing `_agent/`. The error names the file.

## Read next

- `START_HERE.md` — the entry point for the whole method
- `_core/CONVENTIONS.md` — all 22 conventions
- `_core/PACKAGING.md` — the `_agent/` spec and templates
