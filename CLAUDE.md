# Claude Code Dojo

The backing store and knowledge base for the `/dojo` retrospective skill.

## Purpose

Session outcomes depend on both sides — the human and the AI. This repo improves both in tandem. The `/dojo` skill debriefs sessions, surfaces what worked and what didn't, and identifies whether the fix belongs on the Claude side (rules, hooks, skills) or the human side (prompting habits, workflow choices, mental models). Findings that recur graduate into actionable changes for whichever side needs them.

The `/dojo` skill source lives in `skills/dojo.md`, symlinked to `~/.claude/commands/dojo.md`.

## Repository Structure

```
CLAUDE.md                      # This file
skills/
  dojo.md                      # /dojo skill source (symlinked to ~/.claude/commands/dojo.md)
learnings/
  effective-patterns.md        # Proven techniques worth reusing
  anti-patterns.md             # Things that don't work — consult before trying new approaches
  open-questions.md            # Hypotheses under evaluation
domains/                       # Created on demand by /dojo when domain-specific content emerges
```

## Working Here

- **Before writing any entry:** Read existing entries to avoid duplication. Update existing entries when new evidence refines them.
- **Entry quality bar:** Every entry must be specific enough to change behavior — whether that's a future Claude instance or the user. No vague advice.
- **Learnings templates:** Follow the entry format defined at the top of each `learnings/` file.
- **Anti-pattern "Rule" field:** Contains the concrete CLAUDE.md instruction candidate. When a pattern recurs across sessions, graduate the rule to `~/.claude/CLAUDE.md`.
- **Effective-pattern "Audience" field:** Clarifies whether the entry teaches the user, instructs Claude, or both.
- **Domain files:** Created on demand by `/dojo` when a topic accumulates 3+ related entries that don't fit cleanly in the general learnings files (e.g., a specific framework, language, or tool). No rigid template — let structure emerge from content.
- **References:** Fetch from `https://code.claude.com/docs/en/*.md` (index at `https://code.claude.com/docs/llms.txt`) when proposing a rule that may overlap with official best practices, or when resolving an open question that Anthropic docs might address.
