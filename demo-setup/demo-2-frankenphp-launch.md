# Demo 2: GitHub Issue #7424 - FrankenPHP Launch Error

**Issue:** `ddev launch` (HEAD) error with FrankenPHP
**Time:** 12 minutes (including Q&A)  
**Branch:** `demo/frankenphp-launch`

## Pre-Demo Setup

```bash
cd ddev-demo
git checkout demo/frankenphp-launch
code cmd/ddev/cmd/launch.go  # Open the launch command
```

## Demo Script

### 1. Explain the Issue (2 minutes)

**Say:** "Issue #7424 reports that the `ddev launch` command fails when using FrankenPHP as the web server. This is a bug affecting users who want to use modern PHP implementations."

**Show:** 
- Navigate to the GitHub issue
- Explain FrankenPHP (modern PHP server built with Go and Caddy)
- Show the error scenario

### 2. Reproduce the Bug (1 minute)

**Claude Code Query:**
```
"Help me understand how the ddev launch command works and where it might fail with FrankenPHP. Show me the launch command implementation."
```

**Expected Response:** Claude should identify:
- Launch command structure
- How it detects web server URLs
- Potential FrankenPHP-specific issues

### 3. Analyze the Problem (2 minutes)

**Claude Code Query:**
```
"Analyze this launch command code for FrankenPHP compatibility issues. FrankenPHP uses different port/URL patterns than traditional Apache/Nginx. What could be causing the launch to fail?"
```

**Expected Analysis:**
- URL detection logic
- Port number assumptions  
- Web server type detection
- Error handling gaps

### 4. Debug with AI Assistance (3 minutes)

**Step 1:** Identify the failure point
**Claude Code Query:**
```
"Add debug logging to the launch command to identify exactly where it fails with FrankenPHP. Use DDEV's util.Debug() pattern."
```

**Step 2:** Analyze FrankenPHP specifics
**Claude Code Query:**
```
"How does FrankenPHP differ from Apache/Nginx in terms of URL structure and port usage? What should the launch command check for?"
```

**Step 3:** Implement the fix
**Claude Code Query:**
```
"Fix the launch command to properly detect and handle FrankenPHP URLs. Ensure backward compatibility with existing web servers."
```

### 5. Test the Solution (2 minutes)

**Claude Code Query:**
```
"Generate tests for the launch command fix, including test cases for FrankenPHP, Apache, and Nginx to ensure we didn't break existing functionality."
```

**Show:** Walk through the test cases and verify the fix works

### 6. Validate Edge Cases (1 minute)

**Claude Code Query:**
```
"What edge cases should we consider for the FrankenPHP launch fix? Generate additional test scenarios."
```

**Expected Edge Cases:**
- Custom ports
- HTTPS configurations  
- Multiple services
- Container networking issues

### 7. Q&A and Discussion (1 minute)

**Potential Questions:**
- How do we ensure compatibility with future web servers?
- Should this be configurable?
- What about other FrankenPHP-specific features?

## Key Teaching Points

1. **AI excels at debugging** when given specific error contexts
2. **Root cause analysis** benefits from AI's pattern recognition
3. **Backward compatibility** is crucial in bug fixes
4. **Comprehensive testing** prevents regressions

## Technical Details

**FrankenPHP Specifics:**
- Built with Go and Caddy
- Different default port patterns
- Modern HTTP/2 and HTTP/3 support
- Different URL structure conventions

**DDEV Launch Command:**
- Detects running web services
- Constructs URLs based on server type
- Opens browser to project URL
- Handles multiple service scenarios

## Backup Materials

- Pre-recorded debug session
- Screenshots of error messages
- Code diff showing the fix
- Test output examples

## Notes for Presenter

- Emphasize the debugging workflow with AI
- Show how Claude Code can understand different web server architectures
- Highlight the importance of maintaining backward compatibility
- Be prepared to explain FrankenPHP if audience is unfamiliar