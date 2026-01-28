# Serena MCP Setup Guide

This skill requires **Serena MCP** for semantic code navigation. Follow these steps to configure it.

## Prerequisites

- Claude Code CLI installed
- Python with `uv` package manager
- A project with supported languages (PHP, TypeScript, Python, Go, etc.)

## Installation

### 1. Install uv (if not installed)

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### 2. Add Serena MCP Server

Run this command **from your project root**:

```bash
claude mcp add serena -- uvx --from git+https://github.com/oraios/serena serena start-mcp-server --context ide-assistant --project $(pwd)
```

This registers Serena as an MCP server in Claude Code.

### 3. Enable the Server

Add to `.claude/settings.local.json`:

```json
{
  "enabledMcpjsonServers": ["serena"]
}
```

### 4. Configure Permissions

Add Serena tools to your allowed permissions in `.claude/settings.local.json`:

```json
{
  "permissions": {
    "allow": [
      "mcp__serena__get_symbols_overview",
      "mcp__serena__find_symbol",
      "mcp__serena__find_referencing_symbols",
      "mcp__serena__search_for_pattern",
      "mcp__serena__list_dir",
      "mcp__serena__find_file",
      "mcp__serena__list_memories",
      "mcp__serena__read_memory",
      "mcp__serena__replace_symbol_body",
      "mcp__serena__insert_before_symbol",
      "mcp__serena__insert_after_symbol"
    ]
  }
}
```

### 5. Run Onboarding

Ask Claude: **"Run Serena onboarding for this project"**

This is an **interactive process** where Claude will:
1. Analyze your project structure, configs, and code
2. Identify tech stack, conventions, and commands
3. Create memory files in `.serena/memories/`

Typical memories created:
- `project_overview.md` - Purpose, tech stack, features
- `architecture.md` - Code structure, patterns, layers
- `code_style_conventions.md` - Naming, types, formatting rules
- `suggested_commands.md` - Test, lint, build commands
- `task_completion_checklist.md` - What to do before committing

The process may take a few minutes as Claude explores your codebase.

### 6. Disable Auto-Open Dashboard (Optional)

Serena opens a web dashboard by default. To disable auto-open, edit `~/.serena/serena_config.yml`:

```yaml
web_dashboard: true
web_dashboard_open_on_launch: false  # <-- Change this to false
```

The dashboard remains available at http://localhost:24282/dashboard/ when needed.

## Configuration Files

**Global config:** `~/.serena/serena_config.yml`
- Dashboard settings
- Log level
- Tool timeout
- Registered projects

**Project config:** `.serena/project.yml`
- Language servers (php, typescript, python, etc.)
- File encoding
- Ignored paths
- Read-only mode

**Project memories:** `.serena/memories/`
- Automatically generated during onboarding
- Can be manually edited or added

## Verification

After setup, verify Serena is working:

1. Run: `claude mcp list` - Should show serena as connected
2. Ask Claude: "List available Serena memories"
3. Expected: Claude uses `mcp__serena__list_memories` tool

## Supported Languages

Serena uses Language Server Protocol (LSP). Supported languages:

- PHP (via intelephense)
- TypeScript/JavaScript (via typescript-language-server)
- Python (via pylsp or jedi)
- Go (via gopls)
- Rust (via rust-analyzer)
- C/C++ (via clangd)
- Java, Kotlin, Scala
- And more...

## Troubleshooting

### "Serena tools not available"

1. Check if server is enabled in `settings.local.json`
2. Verify MCP was added: `claude mcp list`
3. Restart Claude Code

### "Symbol not found"

1. Ensure file isn't in `.gitignore`
2. Check language server is configured in `.serena/project.yml`
3. Try `substring_matching: true` for partial matches

### Slow Performance

1. Use `relative_path` parameter to restrict searches
2. Use `include_body: false` when you don't need implementation
3. Clear cache: `rm -rf .serena/cache/`

### Multiple Dashboard Windows

Serena may start multiple instances. Use higher ports if needed:
- http://localhost:24282/dashboard/
- http://localhost:24283/dashboard/
- http://localhost:24284/dashboard/

## Resources

- [Serena GitHub](https://github.com/oraios/serena)
- [Serena Documentation](https://oraios.github.io/serena/)
- Project-specific guide: `.claude/docs/serena-mcp-guide.md`
