# Coding Agent Skills

A collection of skills for [Coding Agents](https://agentskills.io) that extend AI capabilities for software development workflows.

## What are Skills?

Skills are auto-invoked prompts that guide the coding agents to use specialized tools and follow best practices for specific tasks. Each skill is a self-contained module with documentation, setup instructions, and workflows.

## Available Skills

| Skill | Description |
|-------|-------------|
| [read-codebase](read-codebase/) | Semantic code exploration using Serena MCP for intelligent navigation |

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/devitools/skills.git
   ```

2. Copy the desired skill folder to your project's `.claude/skills/` directory:
   ```bash
   cp -r skills/read-codebase /path/to/your-project/.claude/skills/
   ```

3. Follow the skill's `setup.md` for any additional configuration.

## Skill Structure

Each skill follows this structure:

```
skill-name/
├── SKILL.md        # Main skill definition with frontmatter
├── setup.md        # Installation and configuration guide
└── workflows.md    # Detailed usage workflows (optional)
```

### SKILL.md Frontmatter

```yaml
---
name: skill-name
description: Brief description of what the skill does
user-invocable: false  # true if can be triggered via /skill-name
---
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on creating and submitting new skills.

## License

MIT License - see [LICENSE](LICENSE) for details.
