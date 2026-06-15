# claude-gitnexus

Portable **global Claude Code config** — the `CLAUDE.md` preferences and custom skills that make my AI workflow reproducible on any machine, instead of re-deriving it per project. Clone this, drop the files into `~/.claude/`, and every project/session picks them up.

This repo holds the **generic, reusable** patterns only — no project- or organization-specific names, paths, or credentials. Keep those out of here.

## What's here

```
CLAUDE.md                              # global preferences (loaded every session, all repos)
settings.json                          # model/theme + GitNexus PreToolUse/PostToolUse hooks (machine-specific paths)
skills/
  gitnexus-auto-index/SKILL.md         # index a repo on first need (.gitnexusrc skipSkills + analyze)
  bruno-test-collections/SKILL.md      # Bruno collections instead of curl; register in the app; env setup
  local-repos-toolbox/SKILL.md         # reusable tools toolbox under <source>/local_repos
```

The detail lives in **skills** (loaded on demand), and `CLAUDE.md` only carries one-line triggers — so unused rules don't cost context tokens on every chat.

### CLAUDE.md covers
- **Git commits:** no `Co-Authored-By` trailer; commit under the context-appropriate identity (personal email for personal repos, work email for work repos).
- **GitNexus auto-indexing**, **Bruno test collections**, **reusable local tools** — each a one-line pointer to the matching skill.

## Apply on a new machine

1. `git clone https://github.com/eminmsoysal/claude-gitnexus.git`
2. Copy into your Claude config dir (`~/.claude/`, on Windows `C:\Users\<you>\.claude\`):
   ```bash
   cp claude-gitnexus/CLAUDE.md      ~/.claude/CLAUDE.md
   cp -r claude-gitnexus/skills/*    ~/.claude/skills/
   # settings.json: merge by hand if you already have one (don't blindly overwrite)
   ```
3. Install GitNexus + its base skills/hooks/MCP once: `npx gitnexus setup` (installs the standard `gitnexus-*` skills and the hooks referenced by `settings.json`).
4. Adjust machine-specific paths (see notes).

## Notes

- `settings.json` hook commands point at a `<user>/.claude/hooks/gitnexus/gitnexus-hook.cjs` path — **machine-specific**; `gitnexus setup` regenerates the hook for your user path. Treat the committed `settings.json` as a reference, not a drop-in.
- The standard `gitnexus-*` skills (gitnexus-cli, gitnexus-debugging, …) are **not** committed here — they're installed by `gitnexus setup`. Only the three custom skills above are tracked.
- **Intentionally excluded:** `~/.claude/.credentials.json`, `sessions/`, `projects/` (memory + transcripts), and anything project/organization-specific — credentials and private data don't belong in a shareable config repo.
