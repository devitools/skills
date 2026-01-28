# Code Review Skill

## Overview
This skill enables AI agents to perform thorough, systematic code reviews with focus on correctness, security, maintainability, and best practices. It helps maintain code quality standards and catches issues before they reach production.

## Description
The Code Review skill guides Claude through a comprehensive code review process, analyzing changes for bugs, security vulnerabilities, performance issues, and adherence to coding standards. It emphasizes constructive feedback with actionable suggestions and maintains high signal-to-noise ratio by focusing on genuinely important issues.

## When to Use This Skill
- Reviewing pull requests before merge
- Analyzing code changes for potential issues
- Ensuring adherence to coding standards
- Identifying security vulnerabilities
- Validating architectural decisions
- Checking for proper error handling
- Verifying test coverage for changes

## Setup Instructions

### Prerequisites
- Access to code changes (git diff, PR files)
- Understanding of project coding standards
- Code review tool or git access

### Configuration
Add this skill to your agent configuration:

```json
{
  "name": "code-review",
  "description": "Perform thorough code reviews focusing on quality and security",
  "auto_invoke": true,
  "triggers": [
    "review",
    "code review",
    "check code",
    "look at changes",
    "analyze code"
  ]
}
```

## Workflow

### 1. Preparation Phase

#### Understand the Context
```
a) Review change description/PR title
   - What problem is being solved?
   - What approach was taken?

b) Identify scope of changes
   - Files modified
   - Lines added/removed
   - Components affected

c) Check for tests
   - Are tests included?
   - Do they cover the changes?
```

#### Gather Context
```bash
# View changes
git diff HEAD^

# Check commit messages
git log --oneline -5

# Find related files
grep -r "relatedFunction" --glob "*.js"
```

### 2. Review Categories

#### A. Correctness
- Logic errors and bugs
- Edge case handling
- Null/undefined checks
- Error handling
- Type safety

#### B. Security
- Input validation
- SQL injection prevention
- XSS vulnerabilities
- Authentication/authorization
- Sensitive data exposure
- Dependency vulnerabilities

#### C. Performance
- Inefficient algorithms
- Unnecessary computations
- Memory leaks
- N+1 queries
- Missing indexes

#### D. Maintainability
- Code clarity and readability
- Proper naming conventions
- Code duplication (DRY)
- Complexity (cyclomatic)
- Documentation needs

#### E. Best Practices
- Framework conventions
- Language idioms
- Design patterns
- SOLID principles
- Separation of concerns

### 3. Review Process

#### Step 1: High-Level Review
```
1. Understand the overall change
2. Verify it solves the stated problem
3. Check architectural soundness
4. Identify major issues first
```

#### Step 2: Detailed Line-by-Line Review
```
1. Read each modified file carefully
2. Consider each change in context
3. Look for specific issue categories
4. Note both problems and good practices
```

#### Step 3: Testing Review
```
1. Verify tests exist for new code
2. Check test quality and coverage
3. Ensure edge cases are tested
4. Validate test names and clarity
```

#### Step 4: Integration Review
```
1. Consider impact on existing code
2. Check for breaking changes
3. Verify backward compatibility
4. Review API contracts
```

### 4. Feedback Formulation

#### High Signal Feedback
```
Focus on:
✓ Bugs and logic errors
✓ Security vulnerabilities
✓ Performance problems
✓ Architectural issues
✓ Missing error handling

Avoid commenting on:
✗ Style preferences (unless severe)
✗ Trivial formatting
✗ Personal preferences
✗ Already-addressed issues
```

#### Constructive Comments
```
Good comment structure:
1. What: Identify the specific issue
2. Why: Explain why it's a problem
3. How: Suggest a concrete solution

Example:
"The password is logged at line 45 (What). This exposes 
sensitive data in logs (Why). Consider removing this log 
or masking the password (How)."
```

## Best Practices

### Review Priorities

#### Critical (Must Fix)
- Security vulnerabilities
- Data corruption risks
- Memory leaks
- Breaking changes without migration
- Logic errors causing incorrect behavior

#### Important (Should Fix)
- Error handling gaps
- Performance issues
- Test coverage gaps
- Poor error messages
- Confusing code structure

#### Nice to Have (Consider)
- Code simplification opportunities
- Better naming suggestions
- Additional documentation
- Refactoring possibilities

### Review Techniques

#### Pattern Matching
Look for common anti-patterns:

```javascript
// Missing error handling
async function fetchData() {
  const response = await fetch(url);  // No try-catch
  return response.json();
}

// SQL injection risk
const query = `SELECT * FROM users WHERE id = ${userId}`;  // Unsafe

// Resource leak
const file = fs.openSync(path);
processFile(file);  // Never closed

// Race condition
if (!cache.has(key)) {
  cache.set(key, expensiveOperation());  // Race between check and set
}
```

#### Security Checklist
- [ ] Input validation on all user data
- [ ] Parameterized queries (no string concatenation)
- [ ] Authentication checks on protected routes
- [ ] Authorization for resource access
- [ ] Sensitive data not logged
- [ ] Secure random for security tokens
- [ ] HTTPS for sensitive data transmission
- [ ] Rate limiting on public APIs
- [ ] XSS prevention (output encoding)
- [ ] CSRF protection

#### Code Quality Checklist
- [ ] Functions have single responsibility
- [ ] Clear and descriptive names
- [ ] Reasonable function length (<50 lines)
- [ ] Minimal nesting depth (<4 levels)
- [ ] No magic numbers or strings
- [ ] Proper error messages
- [ ] Consistent with codebase style
- [ ] No commented-out code
- [ ] Dependencies justified

### Language-Specific Considerations

#### JavaScript/TypeScript
```javascript
// Check for:
- Proper async/await error handling
- Type safety (TypeScript)
- Null/undefined handling
- Memory leaks in event listeners
- Proper this binding
- ESLint compliance

// Good pattern
async function safeOperation(): Promise<Result> {
  try {
    const data = await riskyOperation();
    return { success: true, data };
  } catch (error) {
    logger.error('Operation failed', { error });
    return { success: false, error: error.message };
  }
}
```

#### Python
```python
# Check for:
- Proper exception handling
- Type hints (Python 3.5+)
- PEP 8 compliance
- Context managers for resources
- List comprehensions vs loops
- Generator usage for large data

# Good pattern
def safe_operation() -> Result:
    try:
        with open(file_path) as f:
            data = process_data(f.read())
            return Result(success=True, data=data)
    except (IOError, ValueError) as e:
        logger.error(f"Operation failed: {e}")
        return Result(success=False, error=str(e))
```

#### Go
```go
// Check for:
- Proper error handling (check all errors)
- Goroutine leak prevention
- Race condition protection
- Resource cleanup (defer)
- Context usage for cancellation
- Idiomatic Go patterns

// Good pattern
func safeOperation(ctx context.Context) (*Result, error) {
    select {
    case <-ctx.Done():
        return nil, ctx.Err()
    default:
    }
    
    result, err := riskyOperation()
    if err != nil {
        return nil, fmt.Errorf("operation failed: %w", err)
    }
    
    return result, nil
}
```

## Configuration Examples

### Example 1: Strict Security Review
```json
{
  "skills": [
    {
      "name": "code-review",
      "enabled": true,
      "config": {
        "priority": "security",
        "strict_mode": true,
        "focus_areas": [
          "input_validation",
          "sql_injection",
          "xss",
          "authentication"
        ]
      }
    }
  ]
}
```

### Example 2: Balanced Review
```json
{
  "skills": [
    {
      "name": "code-review",
      "enabled": true,
      "config": {
        "categories": [
          "correctness",
          "security",
          "maintainability",
          "performance"
        ],
        "min_severity": "important",
        "suggest_improvements": true
      }
    }
  ]
}
```

### Example 3: Performance-Focused Review
```json
{
  "skills": [
    {
      "name": "code-review",
      "enabled": true,
      "config": {
        "priority": "performance",
        "check_complexity": true,
        "flag_n_plus_one": true,
        "memory_analysis": true
      }
    }
  ]
}
```

## Common Review Scenarios

### Scenario 1: API Endpoint Addition
```
Review checklist:
1. Input validation for all parameters
2. Authentication/authorization checks
3. Proper HTTP status codes
4. Error handling and messages
5. Rate limiting consideration
6. Tests for success and error cases
7. API documentation updated
```

### Scenario 2: Database Schema Change
```
Review checklist:
1. Migration scripts included
2. Rollback plan documented
3. Indexes for query performance
4. Data integrity constraints
5. Backward compatibility
6. Testing with production-like data
```

### Scenario 3: Security-Sensitive Code
```
Review checklist:
1. No hardcoded secrets
2. Cryptographically secure randomness
3. Proper password hashing (bcrypt, argon2)
4. Token expiration and validation
5. Audit logging for sensitive operations
6. HTTPS enforcement
7. Security tests included
```

## Review Comment Templates

### Bug/Logic Error
```
🐛 **Potential Bug**: [Brief description]

**Issue**: [Explain the problem]
**Impact**: [What could go wrong]
**Suggestion**: [How to fix]

```
Example:
```javascript
// Line 42
const result = arr.find(x => x.id === id);
return result.name;  // 🐛 Potential null reference

// Suggestion: Add null check
const result = arr.find(x => x.id === id);
if (!result) {
  throw new Error(`Item with id ${id} not found`);
}
return result.name;
```

### Security Vulnerability
```
🔒 **Security Issue**: [Brief description]

**Vulnerability**: [Type of security issue]
**Risk**: [Potential impact]
**Fix**: [How to address]

```
Example:
```python
# Line 67
query = f"SELECT * FROM users WHERE name = '{user_input}'"  # 🔒 SQL Injection

# Fix: Use parameterized query
query = "SELECT * FROM users WHERE name = ?"
cursor.execute(query, (user_input,))
```

### Performance Issue
```
⚡ **Performance Concern**: [Brief description]

**Issue**: [What's inefficient]
**Impact**: [Performance implication]
**Optimization**: [Better approach]

```
Example:
```javascript
// Line 89
users.forEach(user => {
  const orders = db.getOrders(user.id);  // ⚡ N+1 query problem
});

// Optimization: Batch load
const userIds = users.map(u => u.id);
const allOrders = db.getOrdersByUserIds(userIds);
```

### Maintainability Suggestion
```
🔧 **Maintainability**: [Brief description]

**Current**: [What's there now]
**Suggestion**: [Improvement]
**Benefit**: [Why it's better]
```

## Tips and Tricks

### Efficient Review Process
1. Start with automated checks (linting, security scanning)
2. Use code_review tool before manual review
3. Review in order: security → correctness → quality
4. Focus on changed lines and their context
5. Consider the bigger picture, not just syntax

### Spotting Hidden Issues
- Check error paths, not just happy paths
- Look at boundaries and edge cases
- Consider concurrency and race conditions
- Think about scale and production load
- Verify proper resource cleanup

### Giving Effective Feedback
- Be specific, not vague
- Provide examples and alternatives
- Explain the "why" behind suggestions
- Acknowledge good code too
- Maintain respectful, collaborative tone

## Integration with Other Skills

Works well with:
- **Testing**: Verify adequate test coverage
- **Semantic Code Navigation**: Understand change context
- **Security Scanning**: Automated vulnerability detection

## Using the code_review Tool

Before finalizing changes:

```javascript
// Call the code_review tool
code_review({
  prTitle: "Add user authentication endpoint",
  prDescription: "Implements JWT-based auth with refresh tokens..."
});

// Review the feedback
// Address legitimate issues
// Re-run if significant changes made
```

## Troubleshooting

### Issue: Too Many Trivial Comments
**Solution**: Raise the severity threshold, focus on critical and important issues only

### Issue: Missing Context for Changes
**Solution**: Read PR description, related issues, and surrounding code for full context

### Issue: Disagreement on Feedback
**Solution**: Explain reasoning clearly, consider codebase conventions, escalate if needed

## Metadata

- **Skill Type**: Code Quality/Review
- **Complexity**: Advanced
- **Prerequisites**: Understanding of language and framework
- **Estimated Setup Time**: 5 minutes
- **Maintenance**: Low - adapt to codebase conventions
