# CLAUDE.md Reference

Source: https://code.claude.com/docs/en/memory
Last updated: 2026-03-10

## File Locations and Scope

| Scope | Location | Shared? |
|---|---|---|
| Managed policy | `/Library/Application Support/ClaudeCode/CLAUDE.md` (macOS) | All users |
| Project | `./CLAUDE.md` or `./.claude/CLAUDE.md` | Team (via git) |
| User | `~/.claude/CLAUDE.md` | Just you |

Parent directory CLAUDE.md files load automatically. Subdirectory CLAUDE.md files load on demand when Claude reads files there.

## Writing Effective Instructions

- Target under 200 lines per file
- Use markdown headers and bullets
- Be specific and verifiable ("Use 2-space indentation" not "Format code properly")
- Avoid contradictions across files — Claude picks arbitrarily
- Emphasis words ("IMPORTANT", "YOU MUST") improve adherence
- If Claude ignores a rule, the file is probably too long

### What to Include
- Bash commands Claude can't guess
- Code style rules that differ from defaults
- Testing instructions and preferred test runners
- Repo etiquette (branch naming, PR conventions)
- Architectural decisions specific to your project
- Common gotchas or non-obvious behaviors

### What to Exclude
- Anything Claude can figure out by reading code
- Standard language conventions Claude already knows
- Detailed API documentation (link instead)
- Information that changes frequently
- Long explanations or tutorials
- Self-evident practices like "write clean code"

## Imports

Use `@path/to/file` syntax to import additional files. Relative paths resolve relative to the containing file. Max depth: 5 hops.

```
See @README.md for project overview
Personal overrides: @~/.claude/my-project-instructions.md
```

## .claude/rules/

Modular instructions in `.claude/rules/` directory. Can be path-scoped:

```yaml
---
paths:
  - "src/api/**/*.ts"
---
# API rules here
```

Rules without `paths` load at launch. Path-scoped rules load when matching files are read.

## Auto Memory

- Storage: `~/.claude/projects/<project>/memory/`
- `MEMORY.md` first 200 lines loaded every session
- Topic files loaded on demand
- Machine-local, per git repo
- Toggle: `/memory` or `autoMemoryEnabled` setting
- Claude decides what to save based on corrections and preferences
