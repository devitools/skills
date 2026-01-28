# Contributing

## Adding a New Skill

1. Create a folder for your skill at the repository root:
   ```
   your-skill-name/
   ```

2. Create the required `SKILL.md` file with frontmatter:
   ```yaml
   ---
   name: your-skill-name
   description: What the skill does (shown in skill listings)
   user-invocable: false
   ---

   # Skill Title

   Instructions and content for the skill...
   ```

3. Add supporting files as needed:
   - `setup.md` - Installation and configuration instructions
   - `workflows.md` - Detailed usage examples and workflows
   - Other supporting documentation

4. Update the README.md table with your skill

5. Submit a pull request

## Skill Guidelines

- **Focused**: Each skill should do one thing well
- **Self-contained**: Include all necessary documentation
- **Tested**: Verify workflows work as documented
- **Clear**: Write for developers who are new to the skill

## Frontmatter Options

| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Skill identifier (lowercase, hyphenated) |
| `description` | Yes | Brief description for listings |
| `user-invocable` | Yes | If `true`, can be triggered via `/skill-name` |
