# Team setup — admin, once

Deploys the Boom ICM foundation to every member of the Claude Team account and makes it un-overridable.
Source of truth: `github.com/timberbarker/boom-icm-foundation`.

## What one file does

`team/managed-settings.json` delivers four things at the highest precedence tier. Members cannot override any of it.

| # | What | How |
|---|------|-----|
| 1 | The **skill** — `/boom-workspace-builder` appears in everyone's Claude | `extraKnownMarketplaces` + `enabledPlugins` |
| 2 | The **rules** — ICM v2, packaging, triage, voice, no-self-merge — injected into every session | `claudeMd` |
| 3 | A **session nag** when a repo has no conforming root `CLAUDE.md` | `SessionStart` hook |
| 4 | **Guardrails** — denies `git merge`, `gh pr merge`, force-push | `permissions.deny` |

## Step 1 — deploy the settings

**Team / Enterprise (recommended).** claude.ai → Admin → Claude Code → Managed settings. Paste the full contents of `team/managed-settings.json`. Save.

Members pick it up on their next session. The first session shows a one-time approval dialog for the hook and the injected rules; after that it loads silently.

**No admin console, or you want device-level enforcement.** Push the same file via MDM (Intune, Jamf, GPO):

- macOS — `/Library/Application Support/ClaudeCode/managed-settings.json`
- Windows — `C:\Program Files\ClaudeCode\managed-settings.json`
- Linux — `/etc/claude-code/managed-settings.json`

Either route, same file. Don't do both.

## Step 2 — retire the old rollout

This supersedes `boom-foundation@boom` (the `Boom-INC/boom-project-foundation` marketplace). The pasted file already replaces it — it declares only the `boom-icm` marketplace.

To run both side by side instead, add the old entries back to `extraKnownMarketplaces` and `enabledPlugins`. Not recommended: two skills that both claim "structure any Boom project" will compete, and the two methods disagree (`_config/` and pipeline stages vs `_core/` and the Packaging Layer).

## Step 3 — GitHub enforcement

```bash
gh repo edit timberbarker/boom-icm-foundation --template
```

Then in GitHub org settings:

- Register `.github/workflows/boom-icm-check.yml` as an **organization-required workflow**.
- Turn on branch protection for `main` and require the `boom-icm-check` status to pass.

Result: a repo with no conforming root `CLAUDE.md`, or a project missing its `_agent/` folder, cannot merge.

## Step 4 — members do nothing

If Step 1 is live, members install nothing. Send them `team/HOW-TO-USE.md`.

Only if you skipped Step 1:

```bash
/plugin marketplace add timberbarker/boom-icm-foundation
/plugin install boom-icm-foundation@boom-icm
```

## Verify

- [ ] A fresh session shows the one-time approval, then loads quietly.
- [ ] `/plugin` lists `boom-icm-foundation` as enabled.
- [ ] `/boom-workspace-builder` is available in a repo that is not this one.
- [ ] Starting Claude in a repo with no conforming `CLAUDE.md` prints the `[boom-icm]` nag.
- [ ] Asking Claude "what are Boom's standing rules?" returns the ICM v2 set.
- [ ] A PR that breaks root `CLAUDE.md` fails `boom-icm-check`.

## Known limits

- **No per-group targeting.** Managed settings apply to every member uniformly.
- **No shared auto-memory.** Memory is per user, per machine. Shared facts go in `claudeMd` or a repo's `CLAUDE.md`.
- **No "team account root CLAUDE.md."** The `claudeMd` key above is the mechanism.
- **The marketplace repo is personal, not org-owned.** It is public, so this works. Move it to `Boom-INC` and update the `repo` field when you want org ownership and access control.

## Precedence

Managed → CLI flags → project `.claude/settings.local.json` → project `.claude/settings.json` → user `~/.claude/settings.json`.

`CLAUDE.md` files concatenate rather than override: managed → user → project → nested. Closest to the work carries the most weight.
