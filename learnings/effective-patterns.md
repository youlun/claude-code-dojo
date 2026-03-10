# Effective Patterns

Proven techniques worth reusing. Each entry should be specific enough to act on.

<!-- Format:
## Short descriptive title
- **Context:** When/where this applies
- **Pattern:** What to do
- **Why it works:** The mechanism, not just the outcome
-->

## Redirecting Claude to check broader scope
- **Context:** When Claude proposes a local/per-repo solution for something that should be global (gitignore, config, conventions)
- **Pattern:** Ask "wouldn't global be a better option?" or "is there already a global config for this?" — one question redirects Claude to the right layer without needing to explain the full reasoning.
- **Why it works:** Claude knows about config hierarchies but doesn't default to checking them. A short nudge is enough to trigger the right behavior. Over time, anti-pattern entries about this should reduce the need for the nudge.
