# Demo 1: GitHub Issue #5337 - Add-on Dependencies

**Issue:** Allow add-ons to download other add-ons as dependencies
**Time:** 12 minutes (including Q&A)
**Branch:** `demo/addon-dependencies`

## Pre-Demo Setup

```bash
cd ddev-demo
git checkout demo/addon-dependencies
code pkg/ddevapp/addons.go  # Open the relevant file
```

## Demo Script

### 1. Explain the Issue (2 minutes)

**Say:** "Let's look at GitHub issue #5337. Currently, DDEV add-ons can't specify dependencies on other add-ons. If an add-on needs another add-on to work, users have to manually install both. We want to automate this."

**Show:** Navigate to the GitHub issue in browser
- Explain the user story and requirements
- Show current add-on installation process

### 2. Analyze Current State (1 minute)

**Claude Code Query:** 
```
"Explain how DDEV currently handles add-on installation. Show me the key functions and data structures involved."
```

**Expected Response:** Claude should identify:
- `InstallAddon()` function
- Add-on metadata structure
- Current installation workflow

### 3. Design Solution with Claude Code (2 minutes)

**Claude Code Query:**
```
"Help me design a dependency system for DDEV add-ons. The add-on metadata should include a 'dependencies' field, and installation should recursively install dependencies. Follow DDEV's existing patterns."
```

**Expected Response:** Claude should suggest:
- Extending add-on metadata structure
- Dependency resolution algorithm
- Integration with existing installation process

### 4. Implement with AI Assistance (3 minutes)

**Step 1:** Extend add-on metadata
**Claude Code Query:**
```
"Add a dependencies field to the add-on metadata structure in DDEV. Show me the code changes needed."
```

**Step 2:** Implement dependency resolution
**Claude Code Query:**
```
"Implement a function to resolve add-on dependencies recursively, checking for circular dependencies and missing add-ons. Use DDEV's error handling patterns."
```

**Step 3:** Update installation process
**Claude Code Query:**
```
"Modify the InstallAddon function to install dependencies first. Maintain backward compatibility with existing add-ons."
```

### 5. Generate Tests (2 minutes)

**Claude Code Query:**
```
"Generate comprehensive unit tests for the add-on dependency system, including edge cases like circular dependencies and missing dependencies."
```

**Expected Output:** Tests covering:
- Valid dependency chains
- Circular dependency detection
- Missing dependency handling
- Backward compatibility

### 6. Demo the Solution (1 minute)

**Show:** Walk through the implemented code:
- Point out the new dependency field
- Explain the resolution algorithm
- Show test cases

### 7. Q&A and Discussion (1 minute)

**Potential Questions:**
- How does this handle version conflicts?
- What about optional vs required dependencies?
- Performance impact of dependency resolution?

## Key Teaching Points

1. **AI excels at system design** when given clear requirements
2. **Iterative refinement** improves AI suggestions
3. **Testing is crucial** for complex dependency logic
4. **Following project patterns** ensures consistency

## Backup Materials

- Screenshots of key code sections
- Pre-written code snippets for manual typing
- Simplified explanation if Claude Code fails

## Notes for Presenter

- Emphasize how Claude Code understands DDEV's existing patterns
- Show how AI suggestions need human review and refinement
- Highlight the importance of comprehensive testing
- Be prepared to explain dependency resolution concepts if audience needs it