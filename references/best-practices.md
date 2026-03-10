# Best Practices Reference

Source: https://code.claude.com/docs/en/best-practices
Last updated: 2026-03-10

## Core Constraint

Context window fills fast and performance degrades as it fills. Most best practices address this.

## Highest-Leverage Practices

### 1. Give Claude a way to verify its work
- Include tests, screenshots, or expected outputs
- Without verification criteria, Claude produces plausible but potentially wrong output
- UI: use Chrome extension for visual verification
- Verification can be tests, linters, or bash commands

### 2. Explore → Plan → Implement → Commit
- Use Plan Mode (`Shift+Tab`) to separate research from execution
- Skip planning for small, clear tasks (typo fixes, renames)
- Plan when uncertain about approach, multi-file changes, or unfamiliar code

### 3. Be specific in prompts
- Reference specific files, mention constraints, point to example patterns
- "Write a test for foo.py covering the edge case where user is logged out" > "add tests for foo.py"
- Vague prompts are fine for exploration

### 4. Manage context aggressively
- `/clear` between unrelated tasks
- `/compact <instructions>` for targeted compaction
- Use subagents for investigation (separate context)
- Rewind with `Esc+Esc` or `/rewind`

## Common Failure Patterns

| Pattern | Problem | Fix |
|---|---|---|
| Kitchen sink session | Mixing unrelated tasks pollutes context | `/clear` between tasks |
| Repeated corrections | Failed approaches clutter context | After 2 failures, `/clear` + better prompt |
| Over-specified CLAUDE.md | Too long → Claude ignores rules | Prune ruthlessly |
| Trust-then-verify gap | No verification = edge case bugs | Always provide tests/verification |
| Infinite exploration | Unscoped "investigate" fills context | Scope narrowly or use subagents |

## CLAUDE.md Guidelines

- Run `/init` to generate starter, then refine
- Keep short and human-readable
- For each line ask: "Would removing this cause mistakes?" If not, cut it.
- Treat like code: review when things go wrong, prune regularly
- Check into git for team collaboration

## Scaling Patterns

- `claude -p "prompt"` for non-interactive/CI usage
- Multiple sessions for parallel work
- Writer/Reviewer pattern: one session implements, another reviews
- Fan out with `--allowedTools` for batch operations
- `--dangerously-skip-permissions` only in sandboxed containers

## Effective Prompting

- Ask codebase questions like you'd ask a senior engineer
- Use Claude to interview you for complex features (AskUserQuestion tool)
- Use `@file` references, paste images, pipe data in
- Course-correct early with `Esc`, don't let Claude go far off track
