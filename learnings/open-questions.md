# Open Questions

Hypotheses and unresolved ideas under exploration. Entries here are not conclusions — they're active lines of inquiry. Promote to `effective-patterns.md` or `anti-patterns.md` once resolved.

<!-- Format:
## Short descriptive title
- **Hypothesis:** What we think might be true
- **Why it matters:** What changes if this is confirmed or refuted
- **Evidence so far:** Observations, partial results, or references
- **Next step:** What to try next to resolve this
-->

## Is auto-memory sufficient for personal per-project context?
- **Hypothesis:** Auto-memory (`~/.claude/projects/`) combined with global `~/.claude/CLAUDE.md` is enough for personal context without needing a separate local file in the repo.
- **Why it matters:** If sufficient, it's one less file to manage and aligns with official Anthropic conventions. If not, we need to adopt the import pattern (`@~/.claude/project-notes.md` in CLAUDE.md).
- **Evidence so far:** Untested. Chosen as the simpler option to try first.
- **Next step:** Use this approach across several sessions. Watch for: context loss between sessions, preferences not being picked up, or needing to repeat yourself.
