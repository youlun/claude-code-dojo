# Anti-Patterns

Things that don't work, or cause problems. Consult this before trying new approaches to avoid repeating past mistakes.

<!-- Format:
## Short descriptive title
- **Context:** What was being attempted
- **What went wrong:** The specific failure or inefficiency
- **Why:** Root cause if known
- **Instead:** What to do instead
-->

## Assuming conventions without verifying documentation
- **Context:** Creating a `.claude.local.md` file based on assumed naming convention
- **What went wrong:** The file name isn't an official Anthropic convention. Could lead to it being silently ignored or conflicting with future official features.
- **Why:** Claude (and humans) pattern-match from partial knowledge. "settings.local.json exists, so local.md probably works too" — plausible but unverified.
- **Instead:** Before creating any Claude Code configuration file, verify the naming convention against current Anthropic documentation. When in doubt, ask or check the docs first. Applies to any tool or framework, not just Claude Code.
