---
name: local-repos-toolbox
description: "Use when about to write a one-off/throwaway script to extract, decrypt, compute, parse, or transform something out of a project — and it could be reused later. Instead of a temp script, add a reusable functional tool to the local_repos toolbox. Examples: \"decrypt this value\", \"write a quick script to pull X from the DB/config\", \"parse this and compute Y\", \"I need a helper for Z\"."
---

# local_repos toolbox

A personal, reusable tool/snippet toolbox so functional helpers don't get re-derived piecemeal from project repos each time. When you're about to write a throwaway script to extract/compute/transform something that has reuse value, put it here instead.

## Location & shape

`<source>/local_repos` — a **single git repo** (not nested), organized by **functional area**, each tool in its own folder with a short `README.md`.

```
local_repos/
  README.md            # tool index + conventions
  .gitignore           # bin/, obj/, .gitnexus/, etc.
  .gitnexusrc          # { "analyze": { "skipSkills": true } }
  <area>/<tool>/       # functional grouping
    <tool files>
    README.md
```

Example shape: a tool folder holding a small file-based app/script that references a target project's own code (e.g. via a project reference) to compute/transform a value, instead of re-implementing that logic.

## When adding a tool

1. Create `local_repos/<area>/<tool>/` with the tool + a short `README.md` (purpose, usage, gotchas).
2. Tools may reference other repos via absolute paths.
3. Update the root `README.md` tool table.
4. Commit under the context-appropriate identity, no co-author trailer (see the global git rule).
5. Re-run `gitnexus analyze` at the root to keep the index fresh (the `gitnexus-auto-index` skill applies if it's somehow not indexed).

## Why

- **Reusable & token-efficient:** next time the same need comes up, run the existing tool instead of re-reconstructing logic from scratch.
- **Indexed:** GitNexus-indexed so tools are discoverable via the MCP tools.
- Prefer a real tool here over a `.tmp_*` script in a project's working dir.
