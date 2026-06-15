# Global Claude Code preferences

## Git commits

- **Never** add a `Co-Authored-By:` trailer (or any co-author line) to commit messages. I am the sole author on every commit.
- Commit under the **context-appropriate identity**: personal repos use my personal email, work repos use my work email. Set it per-repo (`git config user.email …`) so each repo commits under the right identity — don't override to the wrong one.

These apply to **all** repositories and sessions.

## GitNexus auto-indexing

If you need GitNexus on a repo that isn't indexed yet (MCP / `gitnexus list` don't include it, or no `.gitnexus/` at the root), don't report it as unindexed — use the **`gitnexus-auto-index`** skill to index it first, then proceed.

## Bruno test collections (instead of curl)

When you'd otherwise hand-write `curl` to hit a project's API (smoke tests, repeated checks), or when creating / registering / running Bruno collections, use the **`bruno-test-collections`** skill — it has the full procedure. Don't inline that detail here.

## Reusable local tools

When about to write a one-off/throwaway script to extract, decrypt, compute, or transform something from a project that could be reused, use the **`local-repos-toolbox`** skill instead — it has the toolbox location and conventions. Don't inline that detail here.
