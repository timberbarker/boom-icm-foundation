# Build constraints

## Scope
All Boom projects using this foundation must follow conventions 1-22.

## Not in scope
- Personal scratch workspaces (exempt with _agent/EXEMPT.md)
- Multi-agent frameworks (one agent, folder-based structure only)

## Data policy
Foundation projects touch only internal Boom data by default. Client data projects must define cross-tenant access in _agent/identity.md with explicit approval.

## Quality gates
Before handing off between stages:
- [ ] Stage CONTEXT.md is complete (Purpose/Inputs/Process/Output/Done-looks-like/Failure-modes)
- [ ] Output folder exists and contains deliverables
- [ ] Human review checkpoint completed
- [ ] Next stage inputs are ready

## Tools
- GitHub (source of truth)
- Claude Code (primary agent runtime)
- Claude API for programmatic work
