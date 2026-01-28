# Skills Index

This index provides quick access to all available agent skills with brief descriptions and direct links.

## Core Skills

### 1. Semantic Code Navigation
**File**: [skills/semantic-code-navigation.md](skills/semantic-code-navigation.md)  
**Type**: Navigation/Exploration  
**Complexity**: Intermediate  
**Description**: Navigate and explore codebases intelligently using semantic understanding. Find functions, trace dependencies, and understand code architecture efficiently.

**Quick Start Triggers**: `find`, `locate`, `search`, `where is`, `show me`, `navigate to`

---

### 2. Testing
**File**: [skills/testing.md](skills/testing.md)  
**Type**: Testing/Quality Assurance  
**Complexity**: Intermediate to Advanced  
**Description**: Comprehensive testing workflows covering unit tests, integration tests, and end-to-end testing. Write, run, and analyze tests following industry best practices.

**Quick Start Triggers**: `test`, `tests`, `testing`, `verify`, `validate`, `coverage`

---

### 3. Code Review
**File**: [skills/code-review.md](skills/code-review.md)  
**Type**: Code Quality/Review  
**Complexity**: Advanced  
**Description**: Perform thorough, systematic code reviews focusing on correctness, security, maintainability, and best practices. Catch issues before they reach production.

**Quick Start Triggers**: `review`, `code review`, `check code`, `look at changes`, `analyze code`

---

## Skill Selection Guide

### By Task Type

#### Finding and Understanding Code
- **Semantic Code Navigation**: For exploring codebases, finding implementations, tracing dependencies

#### Ensuring Quality
- **Testing**: For writing and running tests
- **Code Review**: For reviewing changes before merge

#### By Development Phase

##### Planning/Exploration
1. Semantic Code Navigation - Understand existing code
2. Code Review - Review similar implementations

##### Implementation
1. Semantic Code Navigation - Find related code
2. Testing - Write tests (TDD approach)

##### Validation
1. Testing - Run test suites
2. Code Review - Review implementation

##### Pre-Merge
1. Testing - Verify all tests pass
2. Code Review - Final review before merge

### By Programming Language

All skills support multiple languages:
- JavaScript/TypeScript
- Python
- Go
- Java
- Ruby
- C#
- PHP
- And more...

## Skill Combinations

### Effective Skill Workflows

#### Bug Fix Workflow
1. **Semantic Code Navigation** → Find bug location
2. **Testing** → Write test to reproduce
3. **Semantic Code Navigation** → Understand affected code
4. **Testing** → Verify fix with tests
5. **Code Review** → Review changes

#### Feature Development Workflow
1. **Semantic Code Navigation** → Understand existing patterns
2. **Testing** → Write tests first (TDD)
3. **Semantic Code Navigation** → Find integration points
4. **Testing** → Run tests continuously
5. **Code Review** → Review implementation

#### Refactoring Workflow
1. **Semantic Code Navigation** → Find all usages
2. **Testing** → Ensure test coverage exists
3. **Semantic Code Navigation** → Understand dependencies
4. **Testing** → Run tests after changes
5. **Code Review** → Validate refactoring

## Quick Reference

### Configuration Syntax

```json
{
  "skills": [
    {
      "name": "skill-identifier",
      "enabled": true,
      "auto_invoke": true,
      "config": {
        "option": "value"
      }
    }
  ]
}
```

### Common Configuration Options

#### Semantic Code Navigation
- `search_depth`: "full" | "targeted"
- `include_tests`: boolean
- `follow_imports`: boolean
- `directories`: string[]
- `exclude_patterns`: string[]

#### Testing
- `framework`: "jest" | "pytest" | "junit" | etc.
- `run_before_commit`: boolean
- `coverage_threshold`: number
- `test_types`: string[]
- `parallel_execution`: boolean

#### Code Review
- `priority`: "security" | "performance" | "balanced"
- `strict_mode`: boolean
- `min_severity`: "critical" | "important" | "nice-to-have"
- `suggest_improvements`: boolean

## Resources

### Documentation
- [Main README](README.md) - Overview and getting started
- [Contributing Guide](CONTRIBUTING.md) - How to contribute
- [Skill Template](SKILL_TEMPLATE.md) - Template for new skills

### External Links
- [Agent Skills Website](https://agentskills.io)
- [GitHub Repository](https://github.com/devitools/skills)
- [Issue Tracker](https://github.com/devitools/skills/issues)

## Upcoming Skills

Skills currently in development:

- **Debugging**: Systematic debugging workflows
- **Refactoring**: Safe code refactoring
- **Documentation**: Generating and maintaining docs
- **Performance Optimization**: Identifying bottlenecks
- **Security Scanning**: Vulnerability detection
- **API Design**: RESTful API design
- **Database Management**: Schema and query optimization

## Version History

### Current Version: 1.0.0
- Initial release with 3 core skills
- Semantic Code Navigation
- Testing
- Code Review

---

**Last Updated**: January 2026  
**Maintained By**: Devitools Community
