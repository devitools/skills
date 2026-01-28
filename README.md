# Agent Skills Collection

A curated collection of agent skills that extend AI capabilities for software development workflows. Skills are auto-invoked prompts that guide Claude to use specialized tools and follow best practices for specific tasks like semantic code navigation, testing, and code review.

## 🎯 Overview

Agent skills help standardize AI-assisted development by providing structured workflows, best practices, and configuration examples for common development tasks. Each skill includes:

- **Setup Instructions**: Quick start guides for enabling and configuring the skill
- **Detailed Workflows**: Step-by-step processes for executing tasks
- **Configuration Examples**: JSON configurations for different use cases
- **Best Practices**: Guidelines and patterns for optimal results
- **Common Scenarios**: Real-world examples with solutions

## 📚 Available Skills

### [Semantic Code Navigation](skills/semantic-code-navigation.md)
Navigate and explore codebases intelligently using semantic understanding. Find functions, trace dependencies, and understand code architecture efficiently.

**Key Features:**
- Intelligent search strategies
- Parallel search execution
- Dependency tracing
- Context-aware code exploration

**Use Cases:**
- Finding function implementations
- Understanding module structure
- Tracing bug sources
- Discovering related tests

### [Testing](skills/testing.md)
Comprehensive testing workflows covering unit tests, integration tests, and end-to-end testing. Write, run, and analyze tests following industry best practices.

**Key Features:**
- Multiple testing frameworks (Jest, pytest, Go testing, etc.)
- Test-driven development (TDD) support
- Test pattern recognition
- Coverage analysis

**Use Cases:**
- Writing tests for new features
- Debugging failing tests
- Improving test coverage
- Setting up testing infrastructure

### [Code Review](skills/code-review.md)
Perform thorough, systematic code reviews focusing on correctness, security, maintainability, and best practices. Catch issues before they reach production.

**Key Features:**
- Multi-category review (security, performance, correctness)
- Language-specific patterns
- Constructive feedback templates
- High signal-to-noise ratio

**Use Cases:**
- Reviewing pull requests
- Identifying security vulnerabilities
- Ensuring coding standards
- Validating architectural decisions

## 🚀 Quick Start

### 1. Choose a Skill
Browse the available skills and select one that matches your needs.

### 2. Review Setup Instructions
Each skill includes prerequisites and configuration requirements.

### 3. Configure Your Agent
Add the skill configuration to your agent setup:

```json
{
  "skills": [
    {
      "name": "semantic-code-navigation",
      "enabled": true,
      "auto_invoke": true
    }
  ]
}
```

### 4. Start Using
Trigger the skill with natural language or let it auto-invoke based on your task context.

## 💡 Usage Examples

### Example 1: Finding Code
```
User: "Where is the authenticateUser function defined?"

Agent: [Uses Semantic Code Navigation skill]
- Searches for function definition
- Identifies file and line number
- Provides surrounding context
```

### Example 2: Writing Tests
```
User: "Add tests for the new payment processing feature"

Agent: [Uses Testing skill]
- Reviews existing test patterns
- Creates test file with proper structure
- Writes comprehensive test cases
- Runs tests to verify
```

### Example 3: Reviewing Changes
```
User: "Review this pull request for issues"

Agent: [Uses Code Review skill]
- Analyzes code changes
- Checks for security vulnerabilities
- Validates test coverage
- Provides actionable feedback
```

## 🛠️ Configuration

### Basic Configuration
```json
{
  "skills": [
    {
      "name": "semantic-code-navigation",
      "enabled": true,
      "auto_invoke": true,
      "triggers": ["find", "locate", "search", "where is"]
    },
    {
      "name": "testing",
      "enabled": true,
      "auto_invoke": true,
      "triggers": ["test", "verify", "validate"]
    },
    {
      "name": "code-review",
      "enabled": true,
      "auto_invoke": true,
      "triggers": ["review", "check code", "analyze"]
    }
  ]
}
```

### Advanced Configuration
```json
{
  "skills": [
    {
      "name": "semantic-code-navigation",
      "enabled": true,
      "config": {
        "search_depth": "full",
        "include_tests": true,
        "follow_imports": true,
        "directories": ["src/", "lib/"],
        "exclude_patterns": ["node_modules", "dist"]
      }
    },
    {
      "name": "testing",
      "enabled": true,
      "config": {
        "framework": "jest",
        "run_before_commit": true,
        "coverage_threshold": 80,
        "test_types": ["unit", "integration"]
      }
    },
    {
      "name": "code-review",
      "enabled": true,
      "config": {
        "categories": ["correctness", "security", "performance"],
        "min_severity": "important",
        "suggest_improvements": true,
        "strict_mode": false
      }
    }
  ]
}
```

## 📖 Best Practices

### Skill Selection
- Use **Semantic Code Navigation** when exploring unfamiliar code
- Use **Testing** when adding features or fixing bugs
- Use **Code Review** before merging changes
- Combine skills for comprehensive workflows

### Effective Usage
1. **Be Specific**: Clear requests yield better results
2. **Provide Context**: Share relevant information about your goals
3. **Iterate**: Refine requests based on initial results
4. **Validate**: Always verify AI-generated code and suggestions

### Combining Skills
Skills work best when used together:
- Navigate to relevant code → Write tests → Review changes
- Find bug location → Write test to reproduce → Fix and review
- Explore API → Understand usage → Add tests → Review implementation

## 🤝 Contributing

We welcome contributions! To add a new skill:

1. **Create Skill Document**: Use the [skill template](SKILL_TEMPLATE.md)
2. **Follow Structure**: Include all required sections
3. **Provide Examples**: Real-world scenarios and configurations
4. **Test Thoroughly**: Validate workflows with actual use cases
5. **Submit PR**: Include documentation and examples

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

## 📋 Skill Template

When creating new skills, follow this structure:

- **Overview**: Brief description
- **Description**: Detailed explanation
- **When to Use**: Applicable scenarios
- **Setup Instructions**: Prerequisites and configuration
- **Workflow**: Step-by-step process
- **Best Practices**: Guidelines and patterns
- **Configuration Examples**: JSON configurations
- **Common Scenarios**: Real-world examples
- **Tips and Tricks**: Advanced usage
- **Integration**: How it works with other skills
- **Troubleshooting**: Common issues and solutions
- **Metadata**: Complexity, prerequisites, maintenance level

## 🗺️ Roadmap

Upcoming skills in development:

- **Debugging**: Systematic debugging workflows and tools
- **Refactoring**: Safe code refactoring with automated testing
- **Documentation**: Generating and maintaining code documentation
- **Performance Optimization**: Identifying and fixing performance bottlenecks
- **Security Scanning**: Automated security vulnerability detection
- **API Design**: RESTful API design and implementation
- **Database Management**: Schema design and query optimization

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🔗 Links

- **Documentation**: [Full documentation](https://agentskills.io)
- **Issues**: [Report bugs or request features](https://github.com/devitools/skills/issues)
- **Discussions**: [Community discussions](https://github.com/devitools/skills/discussions)

## 🙏 Acknowledgments

Thank you to all contributors who help improve these skills and make AI-assisted development more effective and standardized.

---

**Made with ❤️ by the Devitools community**
