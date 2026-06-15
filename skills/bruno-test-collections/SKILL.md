---
name: bruno-test-collections
description: "Use when creating, registering, or running Bruno API test collections for a project — instead of hand-writing curl for smoke tests/repeated API checks. Covers placing the collection in the bruno-tests area, registering it in the Bruno desktop app sidebar, and setting up its environment. Examples: \"add a Bruno test for this endpoint\", \"I keep curling this API\", \"make this collection show up in Bruno\", \"run the bruno tests\"."
---

# Bruno test collections

Prefer a **Bruno** collection over hand-written `curl` when hitting a project's API (smoke tests, repeated checks, reproducing a request): saved `.bru` requests carry known-good headers/body, reproduce real client behavior, and cost fewer tokens on reuse.

## Where they live

`<repos>/bruno-tests/<project>/` — one folder per project under a single `bruno-tests` container dir (the container is not a repo). Each project subfolder is its **own git repo + GitNexus index**.

## Running tests (bru CLI)

```bash
cd <repos>/bruno-tests/<project>
bru run                                  # whole collection
bru run "<folder>/<request>.bru"         # single request
bru run --env <env-name>                 # with an environment
bru run --output results.json            # machine-readable results
```

A project can run its collection here and read pass/fail results instead of reconstructing requests with curl.

## Creating a NEW collection for a project

1. **Place + index:** create it at `<repos>/bruno-tests/<project>/`, `git init`, add `.gitnexusrc` with `{ "analyze": { "skipSkills": true } }`, then `gitnexus analyze` from that folder (the standard skills are already global at `~/.claude/skills/gitnexus-*`).

2. **Register in the Bruno desktop app** (so it shows in the sidebar without manual "Add Collection"):
   - File: `%APPDATA%\bruno\ui-state-snapshot.json`.
   - Add the collection's path (forward-slash form) to `workspaces[0].collections[]`.
   - Add a **minimal** entry to the top-level `collections[]`:
     ```json
     {
       "pathname": "<repos>\\bruno-tests\\<project>",
       "workspacePathname": "<APPDATA>\\bruno\\default-workspace",
       "environment": { "collection": "", "global": "<global-env-id-from-an-existing-entry>" },
       "environmentPath": "",
       "selectedEnvironment": "",
       "isOpen": true,
       "isMounted": true,
       "activeTab": null,
       "tabs": []
     }
     ```
   - **Never force an environment** (`environment`/`selectedEnvironment` stay empty) — forcing one breaks the user's env settings. No tab migration.
   - **Only edit while Bruno is closed** — it rewrites this file on exit and would clobber the edit. Check first (`tasklist | grep -i bruno`). Back it up (`.bak`) before writing.

3. **Set up the environment** the project needs (base URL, keys, etc.) as `environments/<env>.bru` inside the collection — **only if** it doesn't already exist in another collection's environments or in Bruno's global environments (`%APPDATA%\bruno\global-environments.json`). Reuse an existing global env instead of duplicating it.
