# Skills Reference

Source: https://code.claude.com/docs/en/skills
Last updated: 2026-03-10

## What Skills Are

Skills extend Claude's capabilities via `SKILL.md` files. Claude loads them automatically when relevant, or users invoke with `/skill-name`.

Skills replaced custom commands. Files in `.claude/commands/` still work but skills (`.claude/skills/`) are recommended.

## File Structure

```
my-skill/
├── SKILL.md           # Required — main instructions
├── template.md        # Optional supporting files
├── examples/
└── scripts/
```

## Where Skills Live

| Location | Path | Scope |
|---|---|---|
| Enterprise | Managed settings | All users |
| Personal | `~/.claude/skills/<name>/SKILL.md` | All your projects |
| Project | `.claude/skills/<name>/SKILL.md` | This project only |

Precedence: enterprise > personal > project.

Note: `~/.claude/commands/<name>.md` also works for personal skills (flat file, no directory needed).

## Frontmatter

```yaml
---
name: my-skill
description: What this skill does and when to use it
disable-model-invocation: true  # Only user can invoke
user-invocable: false           # Only Claude can invoke
allowed-tools: Read, Grep, Glob # Restrict tool access
model: opus                     # Override model
context: fork                   # Run in subagent
agent: Explore                  # Subagent type (with context: fork)
---
```

## String Substitutions

- `$ARGUMENTS` — all arguments passed
- `$ARGUMENTS[N]` or `$N` — specific argument by index
- `${CLAUDE_SESSION_ID}` — current session ID
- `${CLAUDE_SKILL_DIR}` — directory containing SKILL.md

## Dynamic Context Injection

`` !`command` `` runs a shell command before skill content is sent. Output replaces the placeholder.

```yaml
PR diff: !`gh pr diff`
```

## Invocation Control

| Setting | User can invoke | Claude can invoke |
|---|---|---|
| (default) | Yes | Yes |
| `disable-model-invocation: true` | Yes | No |
| `user-invocable: false` | No | Yes |

## Key Design Notes

- Skill descriptions always in context (so Claude knows what's available)
- Full content only loads when invoked
- Keep SKILL.md under 500 lines
- Use supporting files for detailed reference material
- Description budget: 2% of context window (~16,000 chars fallback)
