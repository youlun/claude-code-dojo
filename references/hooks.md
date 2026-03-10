# Hooks Reference

Source: https://code.claude.com/docs/en/hooks, https://code.claude.com/docs/en/hooks-guide
Last updated: 2026-03-10

## What Hooks Are

User-defined commands that execute at specific points in Claude Code's lifecycle. Unlike CLAUDE.md (advisory), hooks are deterministic — they always run.

## Hook Types

- `command` — shell command (most common)
- `http` — POST to URL
- `prompt` — single-turn LLM evaluation
- `agent` — multi-turn subagent with tool access

## Hook Events

| Event | When | Matcher filters on |
|---|---|---|
| `SessionStart` | Session begins/resumes | `startup`, `resume`, `clear`, `compact` |
| `UserPromptSubmit` | Prompt submitted, before processing | no matcher |
| `PreToolUse` | Before tool executes (can block) | tool name |
| `PermissionRequest` | Permission dialog appears | tool name |
| `PostToolUse` | After tool succeeds | tool name |
| `PostToolUseFailure` | After tool fails | tool name |
| `Notification` | Claude needs attention | notification type |
| `SubagentStart` | Subagent spawned | agent type |
| `SubagentStop` | Subagent finishes | agent type |
| `Stop` | Claude finishes responding | no matcher |
| `InstructionsLoaded` | CLAUDE.md or rule loaded | - |
| `ConfigChange` | Config file changes | config source |
| `PreCompact` | Before compaction | `manual`, `auto` |
| `SessionEnd` | Session terminates | reason |

## Exit Codes

- **0**: action proceeds; stdout added to context (for SessionStart, UserPromptSubmit)
- **2**: action blocked; stderr becomes Claude's feedback
- **Other**: action proceeds; stderr logged (visible in verbose mode)

## Configuration Location

| Location | Scope |
|---|---|
| `~/.claude/settings.json` | All projects |
| `.claude/settings.json` | Single project (shared) |
| `.claude/settings.local.json` | Single project (personal) |
| Managed policy | Organization-wide |

## Common Patterns

### Auto-format after edits
```json
{
  "hooks": {
    "PostToolUse": [{
      "matcher": "Edit|Write",
      "hooks": [{
        "type": "command",
        "command": "jq -r '.tool_input.file_path' | xargs npx prettier --write"
      }]
    }]
  }
}
```

### Desktop notification
```json
{
  "hooks": {
    "Notification": [{
      "matcher": "",
      "hooks": [{
        "type": "command",
        "command": "osascript -e 'display notification \"Claude Code needs attention\" with title \"Claude Code\"'"
      }]
    }]
  }
}
```

### Re-inject context after compaction
```json
{
  "hooks": {
    "SessionStart": [{
      "matcher": "compact",
      "hooks": [{
        "type": "command",
        "command": "echo 'Reminder: use Bun, not npm.'"
      }]
    }]
  }
}
```

### Block protected files
Use `PreToolUse` with `Edit|Write` matcher, check file path, exit 2 to block.

## Prompt-based Hooks

Return `{"ok": true}` or `{"ok": false, "reason": "..."}`. Blocked reasons are fed back to Claude.

## Agent-based Hooks

Like prompt hooks but can read files, run commands. 60s default timeout, up to 50 tool turns.

## Gotchas

- Shell profile `echo` statements break JSON parsing — wrap in `[[ $- == *i* ]]`
- `PostToolUse` hooks can't undo actions
- `PermissionRequest` hooks don't fire in non-interactive mode (`-p`)
- `Stop` hooks need to check `stop_hook_active` to avoid infinite loops
- Hooks added via `/hooks` menu take effect immediately; manual file edits need reload/restart
