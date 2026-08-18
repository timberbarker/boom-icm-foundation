# ICM Packaging Layer

Purpose: ICM covers context. This extends it to cover packaging — capabilities, invocation, isolation and verification. It is an addition to ICM, not a fork. Every existing convention still holds.

## The rule

Every ICM workspace that can be run by anyone other than its author, on any schedule other than a human typing, or against any data other than the author's own, must carry an `_agent/` folder.

Workspaces that fail all three tests are **personal scratch**. They are exempt and should be labelled as such (`_agent/EXEMPT.md`).

## The `_agent/` folder structure

Seven files. One page each. Templates below.

```
_agent/
  definition.md      ← model, owner, what's attached
  connectors.md      ← what servers can reach (allowlist)
  guards.md          ← redaction, logging, approval order
  boundary.md        ← read/write/execute permissions
  identity.md        ← whose data, cross-tenant access
  invocation.md      ← every way a run can start
```

Plus:
```
evals/
  tasks/[slug].md    ← one task per stage + failure tracking
  RESULTS.md         ← running table: task, date, pass/fail
memory/
  durable/           ← knowledge that survives runs
```

## Template: _agent/definition.md

```
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
Tools: [list, or none]
Connectors: [list, or none]
Guards: [ordered list]
Skills: [list]

## Exempt from
[Any convention this workspace does not meet, with reason and review date]
```

## Template: _agent/identity.md

```
# Identity

Runs as: [single author | named team | per tenant]
Tenant source: [where identity comes from]
Credential source: [where secrets come from]

## Data scope
This workspace may touch: [description]
This workspace may not touch: [everything else]

## Cross tenant
Permitted: no | yes, with named exception below
[Exception, reason, approver]
```

## Template: _agent/boundary.md

```
# Boundary

## May read
[Paths inside and outside tree]

## May write
[Paths. Default is workspace tree only]

## May execute
[Commands or none]

## Never
[Explicit denials: credentials, other tenants, production data]
```

## Template: _agent/connectors.md

```
# Connectors

One row per remote surface. No server without an include list.

| Server | Transport | Include only | Used by stage | Auth |
|---|---|---|---|---|
| example-api | http | [tools] | 02-stage | env |

## Denied
[Servers deliberately blocked and why]
```

## Template: _agent/guards.md

```
# Guards

Ordered. Top runs first. Never reorder without noting why.

1. Redact. [Patterns and replacements]
2. Log. [What captured, where, what never logged]
3. Meter. [Token accounting, limits]
4. Approve. [Which actions pause for human]
5. Retry. [What retried, how many times]

## Enforcement
[Where each guard is enforced: code, hook, or by hand]
```

## Template: _agent/invocation.md

```
# Invocation

| Path | Trigger | Who/what | Auth | Rate |
|---|---|---|---|---|
| Interactive | human in Claude Code | [names] | session | n/a |
| Scheduled | cron [expression] | system | service | [limit] |
| Dashboard | user action | tenant user | token | [limit] |
| Webhook | inbound event | [source] | signed | [limit] |

## Not permitted
[Paths that must not exist]
```

## Template: evals/tasks/[slug].md

```
# Task: [name]

Origin: [production failure date, or designed]
Stage under test: [stage]
Input: [file or inline]
Pass condition: [one unambiguous statement]
Last run: [date, pass/fail]
```

## Using the workspace builder

The workspace-builder scaffolds `_agent/` automatically through stage 03b-packaging:

1. **Stage 01:** Gather intent, owner, timeline, data scope
2. **Stage 02:** Identify stages, systems, touchpoints
3. **Stage 03:** Scaffold folder structure (automated)
4. **Stage 03b:** Scaffold `_agent/` + packaging rules (automated)
5. **Stage 04:** Fill stage contracts per project
6. **Stage 05:** Validate all conventions (automated)

After completion: `_agent/` exists, `evals/tasks/` is seeded, all 22 conventions pass.

## Retrofitting existing workspaces

See Part 4 of BOOM_ICM_COMPLETE_WITH_PACKAGING.md for the five-stage retrofit process (inventory → triage → scaffold → populate → validate).

Start with Bucket A (client-facing), then B (scheduled), then C (internal shared). Never retrofit Bucket D (personal scratch).

## Enforcement

Claude Code stops and asks before proceeding if:
- A stage writes outside tree and `boundary.md` doesn't permit it
- A connector is added not in `connectors.md`
- Workspace handed to client and `identity.md` still says single author
- A schedule is added and `invocation.md` doesn't list it
- `definition.md` names no model
