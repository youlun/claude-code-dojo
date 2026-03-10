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
references/                    # Cached Anthropic documentation (distilled)
  claude-md.md                 # CLAUDE.md and memory system
  skills.md                    # Skills/custom commands spec
  hooks.md                     # Hooks API and patterns
  settings.md                  # Settings and configuration
  best-practices.md            # Official best practices
```

## Working Here

- **Before writing any entry:** Read existing entries to avoid duplication. Update existing entries when new evidence refines them.
- **Entry quality bar:** Every entry must be specific enough that a future Claude instance reading it would change its behavior. No vague advice.
- **Learnings templates:** Follow the entry format defined at the top of each `learnings/` file.
- **Domain files:** No rigid template — let structure emerge from content.
- **References:** Distilled Anthropic docs. Refresh periodically via web fetch.
