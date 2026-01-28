# Contributing to Agent Skills

Thank you for your interest in contributing to the Agent Skills collection! This document provides guidelines and instructions for contributing.

## 🎯 How to Contribute

There are several ways to contribute:

1. **Add New Skills**: Create new skill documents for common development tasks
2. **Improve Existing Skills**: Enhance documentation, add examples, or fix issues
3. **Share Use Cases**: Contribute real-world scenarios and solutions
4. **Report Issues**: Help us identify problems or missing features
5. **Provide Feedback**: Share your experience using the skills

## 📝 Adding a New Skill

### Before You Start

1. **Check Existing Skills**: Make sure a similar skill doesn't already exist
2. **Discuss Your Idea**: Open an issue to discuss the proposed skill
3. **Review the Template**: Familiarize yourself with the [skill template](SKILL_TEMPLATE.md)

### Skill Requirements

A good skill should:

- **Solve a Real Problem**: Address a common development task or workflow
- **Be Well-Documented**: Include clear instructions and examples
- **Follow Best Practices**: Demonstrate industry-standard approaches
- **Be Reusable**: Work across different projects and contexts
- **Include Examples**: Provide concrete configuration and usage examples

### Step-by-Step Process

1. **Create the Skill Document**
   ```bash
   cd skills/
   cp ../SKILL_TEMPLATE.md your-skill-name.md
   ```

2. **Fill Out All Sections**
   - Overview and description
   - When to use cases
   - Setup instructions
   - Detailed workflow
   - Best practices
   - Configuration examples
   - Common scenarios
   - Tips and troubleshooting

3. **Add Examples**
   - Include at least 3 real-world scenarios
   - Provide multiple configuration examples
   - Show before/after code samples where applicable

4. **Test Your Skill**
   - Validate all workflows work as described
   - Test configuration examples
   - Verify code samples are correct
   - Check all links and references

5. **Update the Main README**
   - Add your skill to the "Available Skills" section
   - Include a brief description and key features
   - Update any relevant roadmap items

6. **Submit Your PR**
   - Create a pull request with a clear description
   - Reference any related issues
   - Request review from maintainers

## 🔧 Improving Existing Skills

### Types of Improvements

- **Add Missing Information**: Fill in gaps in documentation
- **Update Examples**: Add new configuration examples or scenarios
- **Fix Issues**: Correct errors or outdated information
- **Enhance Clarity**: Improve wording, organization, or formatting
- **Add Language Support**: Extend examples to more programming languages

### Making Improvements

1. **Fork the Repository**
2. **Create a Feature Branch**: `git checkout -b improve-testing-skill`
3. **Make Your Changes**: Edit the relevant skill document
4. **Test Your Changes**: Ensure accuracy and clarity
5. **Submit a PR**: Include a clear description of improvements

## 📚 Documentation Standards

### Writing Style

- **Be Clear and Concise**: Use simple, direct language
- **Be Actionable**: Provide specific steps and examples
- **Be Comprehensive**: Cover common scenarios and edge cases
- **Be Consistent**: Follow the established format and style

### Code Examples

- **Use Standard Formatting**: Follow language-specific conventions
- **Include Comments**: Explain non-obvious code
- **Show Context**: Provide enough surrounding code to understand
- **Test Examples**: Ensure all code examples work correctly

### Markdown Formatting

- Use proper heading levels (H2 for sections, H3 for subsections)
- Use code blocks with language specification: ` ```javascript `
- Use bullet points for lists
- Use tables for structured data
- Use inline code for command names and technical terms

## 🧪 Testing Guidelines

Before submitting a skill or improvement:

### Workflow Testing
- [ ] Test each workflow step manually
- [ ] Verify all commands execute successfully
- [ ] Confirm expected outcomes are achieved

### Configuration Testing
- [ ] Test all configuration examples
- [ ] Verify JSON syntax is valid
- [ ] Ensure configurations are compatible

### Documentation Testing
- [ ] Check all links work correctly
- [ ] Verify code samples are syntactically correct
- [ ] Review for typos and grammatical errors
- [ ] Ensure examples are realistic and practical

## 🎨 Skill Categories

When creating a skill, assign it to one or more categories:

- **Navigation/Exploration**: Finding and understanding code
- **Testing/Quality Assurance**: Writing and running tests
- **Code Quality/Review**: Reviewing and improving code
- **Debugging**: Finding and fixing issues
- **Refactoring**: Improving code structure
- **Documentation**: Creating and maintaining docs
- **Security**: Identifying and fixing vulnerabilities
- **Performance**: Optimizing code and queries
- **Architecture**: Designing systems and components

## 🚀 Pull Request Process

### Before Submitting

1. **Self-Review**: Review your changes carefully
2. **Run Checks**: Ensure markdown is valid
3. **Update Related Docs**: Keep README and other files in sync
4. **Write Clear Commit Messages**: Describe what and why

### PR Description Template

```markdown
## Description
[Briefly describe your changes]

## Type of Change
- [ ] New skill
- [ ] Skill improvement
- [ ] Bug fix
- [ ] Documentation update

## Checklist
- [ ] Follows the skill template structure
- [ ] Includes setup instructions
- [ ] Provides configuration examples
- [ ] Contains real-world scenarios
- [ ] Tested workflows manually
- [ ] Updated main README if needed
- [ ] All links work correctly
- [ ] Code examples are valid

## Related Issues
Closes #[issue number]
```

### Review Process

1. **Automated Checks**: CI will validate markdown and links
2. **Maintainer Review**: A maintainer will review your contribution
3. **Feedback**: Address any requested changes
4. **Approval**: Once approved, your PR will be merged

## 🐛 Reporting Issues

### Bug Reports

When reporting a bug, include:

- **Skill Name**: Which skill has the issue
- **Description**: What's wrong or not working
- **Expected Behavior**: What should happen
- **Actual Behavior**: What actually happens
- **Steps to Reproduce**: How to recreate the issue
- **Environment**: Relevant context (OS, language version, etc.)

### Feature Requests

When requesting a feature, include:

- **Skill Name**: Which skill to enhance (or "New Skill")
- **Problem**: What problem does this solve
- **Proposed Solution**: How should it work
- **Alternatives**: Other approaches considered
- **Use Cases**: When would this be useful

## 💬 Communication

- **GitHub Issues**: For bugs, features, and discussions
- **Pull Requests**: For code/documentation changes
- **Discussions**: For questions and community chat

## 🏆 Recognition

Contributors will be:

- Listed in the main README
- Credited in skill documents they create
- Recognized in release notes
- Invited to become maintainers (for significant contributions)

## 📜 Code of Conduct

### Our Standards

- **Be Respectful**: Treat everyone with respect
- **Be Collaborative**: Work together constructively
- **Be Inclusive**: Welcome diverse perspectives
- **Be Professional**: Maintain professional behavior

### Unacceptable Behavior

- Harassment or discrimination
- Trolling or insulting comments
- Personal or political attacks
- Publishing private information

### Enforcement

Violations may result in:
- Warning
- Temporary ban
- Permanent ban

Report issues to the maintainers.

## ❓ Questions?

If you have questions:

1. Check existing documentation
2. Search closed issues
3. Open a new issue with your question
4. Tag it as "question"

## 🙏 Thank You!

Thank you for contributing to make AI-assisted development better for everyone!

---

**Happy Contributing! 🎉**
