---
name: sync-stitch-react
description: Sync Google Stitch screens into the repo React app using the stitch-react-sync subagent (requires Stitch Instructions + target folder).
---

# Sync Stitch → React (subagent)

Run synchronization of Google Stitch screens into the React app in this repository using the subagent defined in `agents/stitch-react-sync.md` (this plugin).

## 1) Stitch Instructions **and** target folder — gate

**Before any work**, verify the current message (or an explicitly linked file the user attached) contains:

### A) Complete **Stitch Instructions** block

- a section / heading **"Stitch Instructions"** (or an equivalently clear equivalent),
- **Project** — title + **`projectId`** (numeric Stitch project id),
- **Screens** — a **numbered** list: each item has **screen name** + **screen ID** (hex from Stitch).

### B) **Target web folder** (explicit repo-relative path)

- Where to **create or update** the React site — e.g. `docs/website-water` (directory that is or will be the Vite/React app root with `package.json`).

If **anything in (A) or (B) is missing or ambiguous**, **do not proceed** with MCP calls, reading skills, or code edits. Instead **ask the user** (in English, structured):

- for **`projectId`** and **screen id** for every screen to sync,
- include a **short format example** (a "Stitch Instructions" block with Project + numbered Screens),
- for the **target folder**, ask for one unambiguous path if they only said “under docs” or gave no path.

Do not infer ids or folders from indirect context — until the user supplies them in the message or a file, **ask again**.

## 2) Delegate to the subagent

Once Stitch Instructions **and** the target folder are **complete and explicit**, **hand off to** the `stitch-react-sync` subagent:

- The activation payload must include the **verbatim** full Stitch Instructions block (project + all screens).
- The activation payload must include the **target web folder** exactly as the user gave it (repo-relative path).

Example delegation wording (adapt to the actual message):

> Use the **stitch-react-sync** subagent. Follow `agents/stitch-react-sync.md` in the Stitch → React Sync plugin.  
> **Target folder:** `docs/website-water`  
> Here are the Stitch Instructions:  
> [paste full block]

The subagent uses **Stitch MCP** and skills under this plugin’s `skills/` directory; after implementation it must **verify parity** (copy, layout, typography, colors, visuals) with Stitch screens per the agent definition.

## 3) After completion

Summarize the outcome for the user including Stitch ↔ React parity as required by the subagent.
