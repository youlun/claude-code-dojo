# Anti-Patterns

Things that don't work, or cause problems. Consult this before trying new approaches to avoid repeating past mistakes.

<!-- Format:
## Short descriptive title
- **Context:** What was being attempted
- **What went wrong:** The specific failure or inefficiency
- **Why:** Root cause if known
- **Instead:** What to do instead
- **Rule:** Concrete instruction for CLAUDE.md if this recurs. Omit if not applicable.
-->

## Assuming conventions without verifying documentation
- **Context:** Creating a `.claude.local.md` file based on assumed naming convention
- **What went wrong:** The file name isn't an official Anthropic convention. Could lead to it being silently ignored or conflicting with future official features.
- **Why:** Claude pattern-matches from `.local` conventions in other tools (`.env.local`, `settings.local.json`, `docker-compose.override.yml`). This is strong enough that Claude will suggest it even immediately after reading this entry warning against it. The pattern is deeply baked into training data.
- **Instead:** Before creating any Claude Code configuration file, verify the naming convention against current Anthropic documentation. When in doubt, ask or check the docs first. Applies to any tool or framework, not just Claude Code.
- **Rule:** `Before creating any Claude Code config file, verify the naming convention exists in Anthropic docs. Do not infer conventions by analogy from other tools.`

## Proposing per-repo config before checking global scope
- **Context:** Suggesting a `.gitignore` with `.DS_Store` in a specific repo
- **What went wrong:** OS artifacts belong in a global gitignore, not per-repo. Claude jumped to the local solution without checking if a global one existed — which it did, at `~/.config/git/ignore` (XDG convention).
- **Why:** Claude defaults to the most visible/common solution (per-repo `.gitignore`) rather than checking the broader config hierarchy first. Same class of error as suggesting per-project settings when a global setting already handles it.
- **Instead:** Before proposing any config file, check whether a higher-level equivalent already exists (global gitignore, global CLAUDE.md, system-level settings). Work top-down: global → project → local.
- **Rule:** `Before proposing any config file, check if a global/system-level equivalent already exists. Work top-down: global → project → local.`
