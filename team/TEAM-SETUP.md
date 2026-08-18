# Team setup — Owner, once

Deploys the Boom ICM foundation to every member of the Claude Team account and makes it un-overridable.
Source of truth: `github.com/timberbarker/boom-icm-foundation`.

## Before you start

- **Plan:** Claude for Teams or Enterprise. Both support this.
- **Role:** **Owner or Primary Owner.** The plain Admin role cannot see or edit managed settings — the link just bounces you to a different page.
- **Network:** clients need to reach `api.anthropic.com`.
- **Order matters:** the marketplace is read from this repo's **`main` branch**. Merge the rollout PR before you paste the settings, or the plugin won't resolve for anyone.

## What one file does

`team/managed-settings.json` delivers four things at the highest precedence tier. No user, project, or CLI setting can override any of it.

| # | What | Key |
|---|------|-----|
| 1 | The **skill** — `/boom:workspace-builder` appears for everyone | `extraKnownMarketplaces` + `enabledPlugins` |
| 2 | The **rules** — ICM v2, packaging, triage, voice, no-self-merge — injected into every session | `claudeMd` |
| 3 | A **session nag** when a repo has no conforming root `CLAUDE.md` | `hooks.SessionStart` |
| 4 | **Guardrails** — denies `git merge`, `gh pr merge`, force-push | `permissions.deny` |

## Step 1 — merge the rollout PR

The settings point at `main`. Until the plugin structure is on `main`, `enabledPlugins` has nothing to enable.

## Step 2 — paste the settings

Go to **claude.ai → Admin Settings → Claude Code → Managed settings**:

https://claude.ai/admin-settings/claude-code

Paste the full contents of `team/managed-settings.json`. Save.

This **replaces** whatever is in that box — managed sources don't merge. If you already have Boom rules deployed there, this file supersedes them.

Clients pick it up on next startup, or within an hour on an already-running session.

### What your team sees once

Because this ships a hook and a `claudeMd` block, each member gets a one-time security approval dialog naming what's being configured. They must approve. **If someone rejects it, Claude Code exits** — so tell people it's coming and that it's from you.

### Alternative: device-level

If you'd rather push it through MDM (Jamf, Intune, GPO), same file:

- macOS — `/Library/Application Support/ClaudeCode/managed-settings.json`
- Windows — `C:\Program Files\ClaudeCode\managed-settings.json`
- Linux — `/etc/claude-code/managed-settings.json`

Do one or the other, not both. Server-managed wins whenever it delivers any keys at all, and it's the only route that reaches Claude Code on the web.

## Step 3 — retire the old rollout

This supersedes `boom-foundation@boom` (the `Boom-INC/boom-project-foundation` marketplace). The file already handles it — it declares only the `boom-icm` marketplace.

To run both side by side instead, add the old `extraKnownMarketplaces` and `enabledPlugins` entries back. Not recommended: two skills that both claim "structure any Boom project" will compete, and the methods disagree (`_config/` and pipeline stages vs `_core/` and the Packaging Layer).

## Step 4 — GitHub enforcement

```bash
gh repo edit timberbarker/boom-icm-foundation --template
```

Then in GitHub org settings:

- Register `.github/workflows/boom-icm-check.yml` as an **organization-required workflow**.
- Turn on branch protection for `main` and require the `boom-icm-check` status to pass.

Result: a repo with no conforming root `CLAUDE.md`, or a project missing its `_agent/` folder, cannot merge.

## Step 5 — tell the team

Members install nothing. Send them `team/HOW-TO-USE.md`.

Only if you skipped Step 2:

```bash
/plugin marketplace add timberbarker/boom-icm-foundation
/plugin install boom@boom-icm
```

## Verify

Have someone else — not you — restart Claude Code and check:

- [ ] The one-time approval dialog appeared, and after approving, later sessions are quiet.
- [ ] `/status` shows server-managed settings as the active managed source.
- [ ] `/plugin` lists `boom` as enabled.
- [ ] `/boom:workspace-builder` is available in a repo other than this one.
- [ ] Asking "what are Boom's standing rules?" returns the ICM v2 set.
- [ ] Opening a repo with no conforming `CLAUDE.md` prints the `[boom-icm]` nag.
- [ ] A PR that breaks root `CLAUDE.md` fails `boom-icm-check`.

Debug delivery with `claude --debug-file <path>` and search the log for `Remote settings`.

## Known limits

- **No per-group targeting.** Settings apply to every member of the org uniformly.
- **No shared auto-memory.** Memory is per user, per machine. Shared facts go in `claudeMd` or a repo's `CLAUDE.md`.
- **No "team account root CLAUDE.md."** The `claudeMd` key is the mechanism.
- **Not a security boundary.** It's a client-side control. On an unmanaged device a determined user can bypass it without admin rights. Use MDM if you need real enforcement.
- **Doesn't reach third-party providers.** Anyone on Bedrock, Vertex, Foundry, or a custom `ANTHROPIC_BASE_URL` skips the settings fetch entirely.
- **The marketplace repo is personal, not org-owned.** It's public, so this works. Move it to `Boom-INC` and update the `repo` field when you want org ownership and access control.

## Precedence

Server-managed → endpoint-managed (MDM) → CLI flags → project `.claude/settings.local.json` → project `.claude/settings.json` → user `~/.claude/settings.json`.

Within the managed tier there's no merging: the first source that delivers anything wins outright.

`CLAUDE.md` files are different — they concatenate: managed → user → project → nested. Closest to the work carries the most weight.
