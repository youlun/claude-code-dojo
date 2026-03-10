# Claude Code Dojo

The backing store and knowledge base for the `/dojo` retrospective skill.

## Purpose

This repo accumulates learnings about what works and what doesn't when using Claude Code. The `/dojo` skill (available globally) analyzes sessions, identifies patterns, and writes findings here. Over time, these findings feed back into global CLAUDE.md rules, hooks, skills, and configuration — making Claude more effective across all projects.

## Repository Structure

```
CLAUDE.md                      # This file
learnings/
  effective-patterns.md        # Proven techniques worth reusing
  anti-patterns.md             # Things that don't work — consult before trying new approaches
  open-questions.md            # Hypotheses under evaluation
domains/                       # Knowledge per Claude Code capability area
  skills.md                    # Custom slash commands
  hooks.md                     # Event-driven shell commands
  prompting.md                 # CLAUDE.md design and prompt engineering
  configuration.md             # Settings, permissions, MCP servers
  workflows.md                 # Multi-agent orchestration, task decomposition
```

## Working Here

- **Before writing any entry:** Read existing entries to avoid duplication. Update existing entries when new evidence refines them.
- **Entry quality bar:** Every entry must be specific enough that a future Claude instance reading it would change its behavior. No vague advice.
- **Learnings templates:** Follow the entry format defined at the top of each `learnings/` file.
- **Anti-pattern "Rule" field:** Contains the concrete CLAUDE.md instruction candidate. When a pattern recurs across sessions, graduate the rule to `~/.claude/CLAUDE.md`.
- **Effective-pattern "Audience" field:** Clarifies whether the entry teaches the user, instructs Claude, or both.
- **Domain files:** No rigid template — let structure emerge from content.
- **References:** Fetch on demand from `https://code.claude.com/docs/en/*.md`. Index at `https://code.claude.com/docs/llms.txt`.
