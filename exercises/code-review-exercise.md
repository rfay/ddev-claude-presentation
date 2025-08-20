# DDEV Code Review Exercise - AI-Generated Test Improvement

## Objective
Practice reviewing and improving AI-generated code using Claude Code and DDEV standards.

## The Challenge
Review the following AI-generated test code and improve it to meet DDEV quality standards.

## Sample Code to Review
```go
// AI-generated test (needs review)
func TestDatabase(t *testing.T) {
    db := &Database{name: "test"}
    result := db.Connect()
    if result != nil {
        t.Error("failed")
    }
}
```

## Exercise Steps

### Step 1: Initial Review
1. Copy the sample code into Claude Code
2. Ask Claude: "Review this test code for DDEV standards and suggest improvements"
3. Note the issues Claude identifies

### Step 2: Generate Better Tests
1. Ask Claude: "Generate a comprehensive test suite for a database connection function"
2. Compare the new version with the original
3. Ask Claude to explain what makes each test case valuable

### Step 3: Validation
1. Look at existing DDEV tests to verify the patterns match
2. Ask Claude: "How do existing DDEV tests handle similar scenarios?"
3. Refine the tests based on actual DDEV patterns

## Common Issues to Look For
- **Vague assertions:** `if result != nil` without context
- **Missing edge cases:** No error condition testing
- **Poor naming:** Generic variable names
- **Inadequate setup:** Missing test environment preparation
- **No cleanup:** Missing defer statements or cleanup
- **Wrong assertions:** Using basic if statements instead of testify/assert

## Sample Review Prompts
```
"What edge cases are missing from this test?"
"How would DDEV developers write this test?"
"Add proper error handling and assertions"
"Make this test follow table-driven test patterns"
"Show me how DDEV handles test setup and teardown"
```

## Expected Improvements
Your improved test should include:
- Proper table-driven test structure
- Comprehensive edge cases
- Clear, descriptive test names
- Proper setup and teardown
- DDEV-style error handling
- Use of testify/assert or similar

## Success Criteria
- You can identify common AI-generated code issues
- You understand DDEV's testing patterns
- You can improve AI output quality
- You've practiced effective code review prompts

## Time Estimate
8 minutes during presentation, 45 minutes for extended practice

## Real-World Application
This skill directly applies to:
- Reviewing AI-generated code in pull requests
- Improving your own AI-assisted development
- Maintaining code quality in team environments
- Understanding DDEV's quality standards

## Next Steps
After mastering this exercise, try reviewing more complex DDEV code like service implementations or command handlers.