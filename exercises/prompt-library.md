# DDEV + Claude Code Prompt Library

## Navigation & Code Exploration

### Understanding Architecture
```
"Explain how DDEV implements the [specific pattern] with code examples"
"Show me the relationship between [component A] and [component B] in DDEV"
"Walk me through the DDEV startup process step by step"
"How does DDEV handle [specific functionality] internally?"
```

### Finding Code
```
"Find all implementations of [interface name] in the DDEV codebase"
"Show me where DDEV handles [specific error/scenario]"
"Locate the code responsible for [feature] and explain how it works"
"Find examples of [pattern] usage throughout the codebase"
```

### Learning Patterns
```
"What are the common patterns in DDEV's [component] implementations?"
"How should I structure a new [provider/service/command] for DDEV?"
"Show me the conventions for [error handling/configuration/testing] in DDEV"
```

## Development & Implementation

### Code Generation
```
"Generate a new DDEV provider for [platform] following existing patterns"
"Create a command handler for [functionality] that follows DDEV conventions"
"Implement [feature] using DDEV's established patterns and interfaces"
```

### Refactoring
```
"Refactor this code to follow DDEV's Go conventions and patterns"
"Improve this function's error handling using DDEV's util.Error() approach"
"Make this code more consistent with DDEV's existing implementations"
```

### Integration
```
"How would I integrate [technology/service] with DDEV's existing architecture?"
"Show me how to properly extend DDEV's [configuration/service] system"
"What's the correct way to add [functionality] without breaking existing features?"
```

## Testing & Quality

### Test Generation
```
"Generate comprehensive tests for this function including edge cases"
"Create integration tests for this DDEV feature following existing patterns"
"Add unit tests that cover error conditions and boundary cases"
"Generate table-driven tests following DDEV's testing style"
```

### Test Review
```
"Review these tests for completeness and DDEV testing standards"
"What edge cases are missing from this test suite?"
"How can I improve the test coverage for this component?"
"Make these tests follow DDEV's table-driven test patterns"
```

### Quality Assurance
```
"Review this code for DDEV coding standards and suggest improvements"
"Check this implementation for potential issues or edge cases"
"Ensure this code follows DDEV's error handling and logging patterns"
```

## Documentation & Communication

### Code Documentation
```
"Add proper documentation to this function following DDEV's style"
"Generate godoc comments that explain this component's purpose and usage"
"Create inline comments explaining the complex logic in this function"
```

### User Documentation
```
"Write user-facing documentation for this new DDEV feature"
"Create examples showing how to use this new functionality"
"Generate troubleshooting documentation for common issues with [feature]"
```

### API Documentation
```
"Document this API endpoint with examples and error conditions"
"Create configuration documentation for this new option"
"Generate changelog entries for these changes"
```

## Debugging & Problem Solving

### Error Analysis
```
"Analyze this error message and suggest debugging steps"
"What could cause this specific error in DDEV?"
"Walk me through debugging this issue step by step"
"Compare this failing code to working examples in the codebase"
```

### Performance Issues
```
"Identify potential performance bottlenecks in this code"
"How can I optimize this function while maintaining DDEV's patterns?"
"What are the most efficient ways to handle [operation] in DDEV?"
```

### Compatibility
```
"Check this code for cross-platform compatibility issues"
"How does this change affect different DDEV configurations?"
"Ensure this implementation works with all supported [versions/platforms]"
```

## Advanced Prompts

### Context-Rich Requests
```
"Given DDEV's constraint of [specific limitation], how should I implement [feature]?"
"Considering DDEV's goal of [objective], what's the best approach for [problem]?"
"How does this change align with DDEV's architectural principles?"
```

### Iterative Improvement
```
1️⃣ "Add error handling to this function"
2️⃣ "Add DDEV-style error handling with proper error wrapping"
3️⃣ "Add error handling that wraps errors with context and uses DDEV's util.Error() for user-facing messages"
```

### Research-Backed
```
"Research current best practices for [technology] and show how to apply them in DDEV"
"What are the security implications of this approach in DDEV's context?"
"How do other similar tools handle [challenge] and what can DDEV learn?"
```

## Template Patterns

### For New Features
```
"I need to add [feature description] to DDEV. Show me:
1. Where this should be implemented in the codebase
2. What interfaces/patterns I should follow
3. How to structure the code
4. What tests are needed
5. How to document it properly"
```

### For Bug Fixes
```
"I'm seeing [problem description] in DDEV. Help me:
1. Understand what's causing this issue
2. Find the relevant code
3. Identify the root cause
4. Implement a proper fix
5. Add tests to prevent regression"
```

### For Code Review
```
"Review this [component type] implementation for:
1. DDEV coding standards compliance
2. Potential bugs or edge cases
3. Performance considerations
4. Test coverage adequacy
5. Documentation completeness"
```

## Tips for Better Prompts

### Be Specific
- ❌ "Help with DDEV"
- ✅ "Show me how DDEV handles database service configuration"

### Provide Context
- ❌ "Fix this function"
- ✅ "Fix this database connection function to handle timeout errors properly"

### Ask for Explanations
- ❌ "Write code for X"
- ✅ "Write code for X and explain why this approach fits DDEV's architecture"

### Iterate and Refine
- Start broad, then get specific
- Build on previous responses
- Ask follow-up questions for clarity