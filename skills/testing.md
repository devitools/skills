# Testing Skill

## Overview
This skill guides AI agents through comprehensive testing workflows, from writing unit tests to executing test suites and analyzing results. It ensures best practices are followed and helps maintain high code quality.

## Description
The Testing skill enables Claude to create, run, and analyze tests effectively. It covers test-driven development (TDD), behavior-driven development (BDD), and various testing strategies including unit tests, integration tests, and end-to-end tests. The skill helps agents understand testing frameworks, write meaningful test cases, and interpret test results.

## When to Use This Skill
- Writing new tests for features or bug fixes
- Running test suites to verify changes
- Debugging failing tests
- Improving test coverage
- Refactoring tests for better maintainability
- Setting up testing infrastructure
- Analyzing test results and failures

## Setup Instructions

### Prerequisites
- Testing framework installed (Jest, pytest, JUnit, Mocha, etc.)
- Test runner configured in the project
- Access to run commands via bash/shell

### Configuration
Add this skill to your agent configuration:

```json
{
  "name": "testing",
  "description": "Create, run, and analyze tests following best practices",
  "auto_invoke": true,
  "triggers": [
    "test",
    "tests",
    "testing",
    "verify",
    "validate",
    "coverage"
  ]
}
```

## Workflow

### 1. Understanding Testing Requirements
- Identify what needs to be tested
- Determine appropriate test types (unit, integration, e2e)
- Review existing tests for patterns and conventions
- Check for test framework and tooling

### 2. Writing Tests

#### Phase 1: Discover Existing Patterns
```
a) Find existing test files:
   - glob "**/*.test.*" or "**/*.spec.*"
   - Identify test directory structure

b) Read sample tests:
   - Understand testing framework in use
   - Learn project conventions
   - Note assertion styles and helpers

c) Identify test utilities:
   - Mock/stub libraries
   - Test fixtures
   - Custom test helpers
```

#### Phase 2: Create Test Structure
```
a) Follow naming conventions:
   - [name].test.js, [name].spec.ts, [name]_test.go
   - Match source file structure

b) Organize test cases:
   - Group by functionality (describe/context blocks)
   - Use clear, descriptive test names
   - Follow AAA pattern: Arrange, Act, Assert

c) Use appropriate assertions:
   - toBe, toEqual, toThrow for Jest
   - assert.equal, assert.throws for Node assert
   - self.assertEqual, self.assertRaises for pytest
```

#### Phase 3: Write Test Implementation
```
a) Set up test data:
   - Create fixtures or factories
   - Use minimal, focused test data
   - Isolate tests from external dependencies

b) Execute code under test:
   - Call functions/methods with test inputs
   - Simulate user interactions for e2e tests
   - Trigger state changes

c) Assert expected behavior:
   - Verify return values
   - Check state changes
   - Validate side effects
```

### 3. Running Tests

#### Execution Strategy
```
1. Run specific tests first (targeted)
   - Run only the tests related to changes
   - npm test -- path/to/specific.test.js
   - pytest tests/test_specific.py

2. Run test suite for affected area
   - npm test -- --testPathPattern="auth"
   - pytest tests/auth/

3. Run full suite (when confident)
   - npm test
   - pytest
   - go test ./...
```

#### Using Async Mode for Long Tests
```javascript
// Use mode="async" with appropriate initial_wait
bash("npm test", {
  mode: "async",
  initial_wait: 60  // Adjust based on test duration
});

// Follow up with read_bash to get results
read_bash(sessionId, delay: 30);
```

### 4. Analyzing Results
- Review test output for failures
- Identify root causes of failures
- Distinguish between test issues and code issues
- Check for flaky tests
- Analyze coverage reports if available

## Best Practices

### Test Writing Principles

#### 1. Clear and Descriptive Names
```javascript
// Good
test('should return 404 when user does not exist', () => {});
test('should hash password before saving to database', () => {});

// Bad
test('test1', () => {});
test('it works', () => {});
```

#### 2. Test One Thing at a Time
```javascript
// Good - focused test
test('should validate email format', () => {
  const result = validateEmail('invalid');
  expect(result.isValid).toBe(false);
  expect(result.error).toBe('Invalid email format');
});

// Bad - testing too much
test('should handle user registration', () => {
  // Tests validation, database, email sending, etc.
});
```

#### 3. Independent Tests
```javascript
// Good - test is self-contained
beforeEach(() => {
  user = createTestUser();
});

afterEach(() => {
  cleanupTestUser(user);
});

// Bad - tests depend on each other
test('create user', () => { /* saves to shared state */ });
test('update user', () => { /* depends on previous test */ });
```

#### 4. Use Appropriate Mocks
```javascript
// Good - mock external dependencies
jest.mock('./emailService');
const mockSendEmail = emailService.sendEmail;

test('should send welcome email', () => {
  registerUser(userData);
  expect(mockSendEmail).toHaveBeenCalledWith(expect.objectContaining({
    to: userData.email,
    subject: 'Welcome!'
  }));
});
```

### Framework-Specific Patterns

#### Jest (JavaScript/TypeScript)
```javascript
describe('UserService', () => {
  let userService;
  
  beforeEach(() => {
    userService = new UserService();
  });
  
  describe('createUser', () => {
    it('should create user with valid data', () => {
      const userData = { name: 'John', email: 'john@example.com' };
      const result = userService.createUser(userData);
      
      expect(result).toBeDefined();
      expect(result.id).toBeTruthy();
      expect(result.name).toBe(userData.name);
    });
    
    it('should throw error for invalid email', () => {
      const userData = { name: 'John', email: 'invalid' };
      
      expect(() => userService.createUser(userData))
        .toThrow('Invalid email format');
    });
  });
});
```

#### pytest (Python)
```python
import pytest
from myapp.user_service import UserService

class TestUserService:
    @pytest.fixture
    def user_service(self):
        return UserService()
    
    def test_create_user_with_valid_data(self, user_service):
        user_data = {'name': 'John', 'email': 'john@example.com'}
        result = user_service.create_user(user_data)
        
        assert result is not None
        assert result['id'] is not None
        assert result['name'] == user_data['name']
    
    def test_create_user_with_invalid_email_raises_error(self, user_service):
        user_data = {'name': 'John', 'email': 'invalid'}
        
        with pytest.raises(ValueError, match='Invalid email format'):
            user_service.create_user(user_data)
```

#### Go Testing
```go
func TestUserService_CreateUser(t *testing.T) {
    t.Run("creates user with valid data", func(t *testing.T) {
        service := NewUserService()
        userData := UserData{Name: "John", Email: "john@example.com"}
        
        result, err := service.CreateUser(userData)
        
        assert.NoError(t, err)
        assert.NotNil(t, result)
        assert.NotEmpty(t, result.ID)
        assert.Equal(t, userData.Name, result.Name)
    })
    
    t.Run("returns error for invalid email", func(t *testing.T) {
        service := NewUserService()
        userData := UserData{Name: "John", Email: "invalid"}
        
        result, err := service.CreateUser(userData)
        
        assert.Error(t, err)
        assert.Nil(t, result)
        assert.Contains(t, err.Error(), "Invalid email format")
    })
}
```

## Configuration Examples

### Example 1: Basic Testing Setup
```json
{
  "skills": [
    {
      "name": "testing",
      "enabled": true,
      "config": {
        "framework": "jest",
        "run_before_commit": true,
        "coverage_threshold": 80
      }
    }
  ]
}
```

### Example 2: TDD Workflow
```json
{
  "skills": [
    {
      "name": "testing",
      "enabled": true,
      "config": {
        "mode": "tdd",
        "write_tests_first": true,
        "run_on_save": true,
        "watch_mode": false
      }
    }
  ]
}
```

### Example 3: Comprehensive Testing
```json
{
  "skills": [
    {
      "name": "testing",
      "enabled": true,
      "config": {
        "test_types": ["unit", "integration", "e2e"],
        "frameworks": {
          "unit": "jest",
          "integration": "jest",
          "e2e": "playwright"
        },
        "parallel_execution": true
      }
    }
  ]
}
```

## Common Testing Scenarios

### Scenario 1: Adding Tests for New Feature
```
1. Review feature implementation
2. Identify testable components and edge cases
3. Create test file following project conventions
4. Write tests covering:
   - Happy path
   - Edge cases
   - Error conditions
5. Run tests to verify
```

### Scenario 2: Debugging Failing Tests
```
1. Run the specific failing test in isolation
2. Read test code to understand expectations
3. Review implementation for discrepancies
4. Add debug logging if needed
5. Fix issue (in test or code)
6. Re-run to verify fix
```

### Scenario 3: Improving Test Coverage
```
1. Identify untested code paths
2. Analyze complexity and risk
3. Prioritize critical paths
4. Write tests for uncovered areas
5. Run coverage report to verify improvement
```

## Testing Strategies

### Unit Testing
- Test individual functions/methods in isolation
- Mock external dependencies
- Fast execution, no I/O
- High coverage of logic paths

### Integration Testing
- Test interactions between components
- Use real dependencies where practical
- Verify data flow and communication
- Test API endpoints, database queries

### End-to-End Testing
- Test complete user workflows
- Use real or staging environment
- Simulate actual user behavior
- Validate business requirements

### Test-Driven Development (TDD)
```
1. Write failing test (Red)
2. Implement minimum code to pass (Green)
3. Refactor while keeping tests green (Refactor)
4. Repeat
```

## Commands Reference

### JavaScript/Node.js
```bash
# Run all tests
npm test

# Run specific test file
npm test -- path/to/test.js

# Run tests matching pattern
npm test -- --testPathPattern="auth"

# Run with coverage
npm test -- --coverage

# Watch mode
npm test -- --watch
```

### Python
```bash
# Run all tests
pytest

# Run specific test file
pytest tests/test_user.py

# Run specific test
pytest tests/test_user.py::test_create_user

# Run with coverage
pytest --cov=myapp tests/

# Verbose output
pytest -v
```

### Go
```bash
# Run all tests
go test ./...

# Run tests in package
go test ./pkg/user

# Run specific test
go test -run TestCreateUser ./pkg/user

# With coverage
go test -cover ./...

# Verbose output
go test -v ./...
```

## Tips and Tricks

### Running Tests Efficiently
- Use `mode="async"` for long-running test suites
- Set appropriate `initial_wait` (60+ seconds for builds/tests)
- Run targeted tests first, full suite when confident
- Use watch mode during active development

### Handling Flaky Tests
- Identify non-deterministic behavior
- Fix race conditions
- Use proper async/await patterns
- Add explicit waits where needed
- Seed random data for reproducibility

### Test Data Management
- Use factories for creating test objects
- Keep test data minimal and focused
- Use fixtures for reusable setup
- Clean up after tests (in afterEach/teardown)

## Integration with Other Skills

Works well with:
- **Code Review**: Verify tests are included with changes
- **Semantic Code Navigation**: Find related tests for code
- **Debugging**: Use tests to reproduce and isolate issues

## Troubleshooting

### Issue: Tests Timeout
**Solution**: Increase timeout in test configuration or `initial_wait` parameter

### Issue: Tests Pass Locally but Fail in CI
**Solution**: Check for environment-specific dependencies, timing issues, or missing setup

### Issue: Mock Not Working
**Solution**: Ensure mock is set up before importing code under test

## Metadata

- **Skill Type**: Testing/Quality Assurance
- **Complexity**: Intermediate to Advanced
- **Prerequisites**: Testing framework installed
- **Estimated Setup Time**: 10 minutes
- **Maintenance**: Medium - requires framework knowledge
