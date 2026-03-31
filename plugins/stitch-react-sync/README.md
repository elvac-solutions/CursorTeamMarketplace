# Stitch → React Sync (Cursor plugin)

Bundled workflow for synchronizing **Google Stitch** projects into a **Vite/React** app in your repository.

This plugin is published from the [CursorTeamMarketplace](https://github.com/elvac-solutions/CursorTeamMarketplace) monorepo (`plugins/stitch-react-sync/`).

## What is included

| Component | Role |
|-----------|------|
| **`mcp.json`** | Registers the **Stitch MCP** server (`https://stitch.googleapis.com/mcp`). |
| **`skills/`** | `stitch-design`, `react-components`, `design-md`, `enhance-prompt`, `taste-design`, `stitch-loop` — same material as IronScale `.agents/skills/`. |
| **`agents/stitch-react-sync.md`** | Subagent: Stitch MCP + skills + parity verification. |
| **`commands/sync-stitch-react.md`** | Slash command that gates on Stitch Instructions + target folder, then delegates to the subagent. |

## Stitch MCP authentication

The HTTP MCP endpoint requires a **Google API key** with Stitch access. Set it in **Cursor → Settings → MCP**: edit the `stitch` server and add header:

- **`X-Goog-Api-Key`**: your key

Alternatively merge a local override that supplies `headers` for `stitch` (do not commit secrets).

## Usage

1. Enable this plugin in Cursor.
2. Run **`/sync-stitch-react`** (or invoke the command from the palette).
3. Provide a **Stitch Instructions** block (`projectId`, numbered screen IDs) and an explicit **repo-relative** path to the React app root (`package.json`).

The subagent refuses to call MCP or edit code until both are explicit; see `commands/sync-stitch-react.md`.

## Skills path

Inside this plugin, skills live under `skills/<skill-id>/SKILL.md`. The subagent references those paths.
