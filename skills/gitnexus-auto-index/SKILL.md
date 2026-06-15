---
name: gitnexus-auto-index
description: "Use when you need GitNexus for a repository but it is not yet indexed — the MCP tools / `gitnexus list` don't include it, or there's no `.gitnexus/` folder at the repo root. Instead of reporting 'repo not indexed', index it first. Examples: \"GitNexus can't find this repo\", \"impact/query says repo not indexed\", \"use gitnexus on this new repo\"."
---

# GitNexus auto-indexing

When you need GitNexus for a repository but it is **not yet indexed** — the MCP tools / `gitnexus list` don't include it, or there is no `.gitnexus/` folder at the repo root — do NOT tell the user "the repo isn't indexed in GitNexus." Index it yourself first:

1. At the repo's git root, if `.gitnexusrc` does not already exist, create it with exactly:
   ```json
   {
     "analyze": {
       "skipSkills": true
     }
   }
   ```
   (The standard GitNexus skills are already installed globally at `~/.claude/skills/gitnexus-*`, so `skipSkills` just prevents redundant per-repo skill copies. Do **not** add `skipAgentsMd` / `skipContextFiles` — letting it generate `AGENTS.md` / `CLAUDE.md` is fine.)
2. Run `gitnexus analyze` from that repo root.
3. Then proceed with the GitNexus MCP tools normally.

Only do this when GitNexus is actually needed for the task and the path is a git repository. This avoids manually running `gitnexus analyze` in every new repo.
