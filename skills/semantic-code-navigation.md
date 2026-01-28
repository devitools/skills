# Semantic Code Navigation Skill

## Overview
This skill enables AI agents to perform intelligent code navigation and exploration using semantic understanding of the codebase. It helps agents find relevant code, understand dependencies, and trace execution flows.

## Description
The Semantic Code Navigation skill empowers Claude to navigate complex codebases efficiently by understanding the semantic relationships between different code elements. It combines advanced search capabilities with contextual analysis to help locate functions, classes, interfaces, and other code constructs across large projects.

## When to Use This Skill
- Finding the implementation of specific functionality
- Tracing code dependencies and relationships
- Understanding code architecture and structure
- Locating usage examples of APIs or functions
- Discovering test files related to specific modules
- Analyzing cross-file dependencies

## Setup Instructions

### Prerequisites
- Access to the codebase repository
- Search tools enabled (grep, glob, or code search)
- File reading permissions

### Configuration
Add this skill to your agent configuration:

```json
{
  "name": "semantic-code-navigation",
  "description": "Navigate and explore code using semantic understanding",
  "auto_invoke": true,
  "triggers": [
    "find",
    "locate",
    "search",
    "where is",
    "show me",
    "navigate to"
  ]
}
```

## Workflow

### 1. Understanding the Query
- Parse the user's navigation request
- Identify key terms, symbols, or patterns to search for
- Determine the scope (file, directory, entire repository)

### 2. Strategic Search Approach
```
a) Start with targeted searches:
   - Use grep for content patterns
   - Use glob for file name patterns
   - Combine multiple searches in parallel when independent

b) Analyze initial results:
   - Identify relevant files
   - Note patterns in naming or structure
   - Prioritize by relevance

c) Deep dive into promising results:
   - Read relevant files
   - Extract semantic context
   - Follow imports and dependencies
```

### 3. Contextual Analysis
- Understand the role of found code elements
- Identify relationships between components
- Map out the relevant code structure

### 4. Result Synthesis
- Present findings clearly and concisely
- Include file paths and line numbers
- Provide context about how pieces fit together
- Suggest related areas if applicable

## Best Practices

### Search Efficiency
- **Use parallel searches** when looking for multiple independent patterns
- **Start broad, then narrow** when uncertain about exact terms
- **Use glob patterns** for file discovery: `**/*.ts`, `**/test/**`
- **Use grep with context** (`-A`, `-B`, `-C` flags) to understand usage

### Pattern Examples
```bash
# Finding function definitions
grep -n "function handleRequest" --glob "*.js"

# Finding class declarations
grep -n "class.*Component" --glob "*.tsx"

# Finding imports of specific module
grep "import.*from.*'./utils'" --glob "**/*.ts"

# Finding test files for a module
glob "**/user.test.ts"
```

### Navigation Strategies

#### For Finding Implementations
1. Search for function/class definitions
2. Check for interface implementations
3. Look in common directories (src/, lib/, app/)

#### For Understanding Dependencies
1. Find import statements
2. Trace to source files
3. Map the dependency graph

#### For Locating Tests
1. Look for `.test`, `.spec` file patterns
2. Search for describe/it blocks mentioning the feature
3. Check `__tests__` or `test/` directories

## Configuration Examples

### Example 1: Basic Navigation Setup
```json
{
  "skills": [
    {
      "name": "semantic-code-navigation",
      "enabled": true,
      "config": {
        "search_depth": "full",
        "include_tests": true,
        "follow_imports": true
      }
    }
  ]
}
```

### Example 2: Focused Navigation
```json
{
  "skills": [
    {
      "name": "semantic-code-navigation",
      "enabled": true,
      "config": {
        "search_depth": "targeted",
        "directories": ["src/", "lib/"],
        "exclude_patterns": ["node_modules", "dist", "build"]
      }
    }
  ]
}
```

### Example 3: Test-Focused Navigation
```json
{
  "skills": [
    {
      "name": "semantic-code-navigation",
      "enabled": true,
      "config": {
        "primary_focus": "tests",
        "search_patterns": ["*.test.ts", "*.spec.ts", "*_test.go"],
        "link_to_source": true
      }
    }
  ]
}
```

## Common Scenarios

### Scenario 1: Finding a Function Implementation
```
User: "Where is the authenticateUser function defined?"

Agent workflow:
1. grep "function authenticateUser" or "authenticateUser.*=.*function"
2. If multiple results, check each for the actual definition vs. usage
3. Read the file to confirm and provide context
```

### Scenario 2: Understanding a Module's Structure
```
User: "Show me how the auth module is organized"

Agent workflow:
1. glob "**/auth/**/*" to find all auth-related files
2. Read key files (index, main module files)
3. Identify public APIs and internal utilities
4. Present the structure with brief descriptions
```

### Scenario 3: Tracing a Bug to Its Source
```
User: "Find where the validation error is coming from"

Agent workflow:
1. grep "validation error" or error message text
2. Identify the error throwing location
3. Trace back through the call chain
4. Identify the root cause
```

## Tips and Tricks

### Efficient Multi-Pattern Search
When looking for multiple things, search in parallel:
```javascript
// Execute all at once in a single response:
grep("pattern1"); grep("pattern2"); grep("pattern3");
glob("**/*.tsx"); glob("**/*.test.ts");
```

### Handling Large Codebases
- Start with directory-level exploration using `view`
- Use specific glob patterns to reduce search space
- Focus on main entry points and index files first

### Following the Trail
1. Start at entry points (main.ts, index.js, app.py)
2. Follow imports to understand flow
3. Look for middleware, routers, or controllers
4. Trace to business logic and data layers

## Integration with Other Skills

This skill works well with:
- **Code Review**: Navigate to files that need review
- **Testing**: Find tests related to code being modified
- **Refactoring**: Identify all usages of code to be refactored
- **Debugging**: Trace execution paths to find issues

## Troubleshooting

### Issue: Too Many Results
**Solution**: Narrow the search with more specific patterns or directory constraints

### Issue: Can't Find Expected Code
**Solution**: Try variations in naming, check different file extensions, search for related terms

### Issue: Understanding Complex Dependencies
**Solution**: Create a dependency map by systematically following imports

## Examples in Action

### Example 1: Quick Function Lookup
```
User Query: "Find the calculateTotal function"
Agent Action: grep -n "calculateTotal\s*[=(]" --glob "**/*.js"
Result: Found in src/billing/calculator.js:45
```

### Example 2: Module Exploration
```
User Query: "What's in the database module?"
Agent Action: view src/database/ then read key files
Result: Provides overview of connectors, models, migrations
```

### Example 3: Cross-Reference Search
```
User Query: "Find all uses of the User model"
Agent Action: grep "import.*User.*from" --glob "**/*.ts"
Result: Lists 15 files with usage context
```

## Metadata

- **Skill Type**: Navigation/Exploration
- **Complexity**: Intermediate
- **Prerequisites**: Basic code search tools
- **Estimated Setup Time**: 5 minutes
- **Maintenance**: Low - works with standard search tools
