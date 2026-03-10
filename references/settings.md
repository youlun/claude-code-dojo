# Settings Reference

Source: https://code.claude.com/docs/en/settings
Last updated: 2026-03-10

## Configuration Files

```
~/.claude/settings.json              # User settings (all projects)
.claude/settings.json                # Project settings (shared)
.claude/settings.local.json          # Local settings (personal, gitignored)
managed-settings.json                # System-level
```

## Scope Precedence (highest to lowest)

1. Managed (cannot be overridden)
2. Command line arguments
3. Local project settings
4. Shared project settings
5. User settings

## Key Settings

| Key | Description | Example |
|---|---|---|
| `model` | Override default model | `"claude-sonnet-4-6"` |
| `availableModels` | Restrict model selection | `["sonnet", "haiku"]` |
| `language` | Preferred response language | `"japanese"` |
| `outputStyle` | Output style adjustment | `"Explanatory"` |
| `cleanupPeriodDays` | Session cleanup (default: 30) | `20` |
| `env` | Environment variables | `{"FOO": "bar"}` |
| `autoMemoryEnabled` | Toggle auto memory | `false` |
| `alwaysThinkingEnabled` | Extended thinking | `true` |
| `respectGitignore` | Respect .gitignore in file picker | `false` |

## Permission Rules

```json
{
  "permissions": {
    "allow": ["Bash(npm run lint)", "Bash(npm run test *)"],
    "deny": ["Bash(curl *)", "Read(./.env)"]
  }
}
```

Syntax: `ToolName` (all), `ToolName(pattern *)` (prefix match), `ToolName(exact)` (exact).

## Sandbox Configuration

```json
{
  "sandbox": {
    "enabled": true,
    "autoAllowBashIfSandboxed": true,
    "filesystem": {
      "allowWrite": ["//tmp/build"],
      "denyRead": ["~/.aws/credentials"]
    },
    "network": {
      "allowedDomains": ["github.com"]
    }
  }
}
```

Path prefixes: `//` = absolute, `~/` = home, `/` = relative to settings file.

## Other Files

| File | Purpose |
|---|---|
| `~/.claude.json` | Preferences, OAuth, MCP servers, caches |
| `.mcp.json` | Project-scoped MCP servers |
| `~/.claude/agents/` | User subagents |
| `.claude/agents/` | Project subagents |

## Useful

- `/status` shows active settings and their sources
- JSON schema: `"$schema": "https://json-schema.store.org/claude-code-settings.json"`
- Array settings merge across scopes (not replace)
- Automatic timestamped backups (5 most recent)
