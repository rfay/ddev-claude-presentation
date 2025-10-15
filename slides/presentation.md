# DDEV Development with Claude Code
## Training Presentation

<img src="images/ddev-logo.svg" alt="DDEV Logo" class="ddev-logo">

**AI-Assisted Development Workflows**

---

## Table of Contents

<div style="font-size: 0.9em; line-height: 1.6;">

1. **Introduction & Overview**  
   *Setting the context for AI-assisted DDEV development*

2. **About Claude Code**  
   *Understanding Claude Code capabilities and limitations*

3. **Setup & Configuration**  
   *Getting started with DDEV and Claude Code integration*

4. **Technical Workflows**  
   *Navigation, discovery, and development patterns*

5. **Live Demonstrations**  
   *Real DDEV issues and AI-assisted solutions*

6. **Best Practices**  
   *Code quality, testing, and prompt engineering*

7. **Q&A & Resources**  
   *Discussion and follow-up materials*

</div>

---

## Introduction & Overview

Note: Section 1 of 7 - Setting the context for AI-assisted DDEV development

--

### What We'll Work At Today

**Practical AI-Assisted Development Techniques:**

* **Practical workflows** for DDEV development with Claude Code
* **Real-time implementation** of DDEV features and bug fixes
* **Best practices** for AI-assisted development in open source projects
* **Techniques applicable** to your own development projects

---

### Capabilities

- **AI pair programming assistant** and it can do things (that you allow) on your system
- **Context-aware analysis** of large codebases and complex architectures and even adapt to existing style
- **Conversation-based workflow** for iterative development
- **Multi-language expertise** 
- **Real-time assistance/collaboration** for coding, debugging, testing, and documentation

---

#### Key Strengths

- **Pattern recognition** in existing codebases
- **Code generation** following established conventions
- **Test creation** with comprehensive edge case coverage
- **Documentation writing** in multiple formats (questionable)
- **Debugging assistance** with error analysis and solutions

---

#### Claude Limitations

- **Context windows** - works best with focused, specific tasks  
- **Knowledge cutoff** - may not know about very recent changes
- **Hallucination risk** - always verify generated code
- **Limited time usage** - they shut you off after unclear time, and you don't get to start again until later

---


### Getting Started

- DDEV installed and working
- VS Code or JetBrains IDE (or no IDE at all)
- Git and GitHub CLI (optional but recommended)
- Claude Code installed and working 
- Claude Code/Anthropic account
- Basic Go and DDEV architecture knowledge

---

### Basic Benefits

- Claude gives you a real chance to describe a problem or feature in careful detail, letting you think about and design the problem in advance. Use that, it helps you! And then it helps Claude.
- Being able to take on a problem using Claude has me far more willing to start on something I don't completely understand.
- For more complex problems or features, describe the solution to Claude in detail and ask it to write a PRD.
- Use git commits to keep track of where you are and be able to revert if things go bad. You can have Claude make commits with detailed messages.
- I've been very happy with these organizational principles.

### Strategies to Get The Most Value
- DDEV has a CLAUDE.md with basic instructions, you may need to adapt (but it's not very obedient)
- Static analysis and tests are a great way to keep Claude "on the rails"

---

## Technical Workflows

Note: Section 4 of 7 - Navigation, discovery, and development patterns

--

### Codebase Navigation

#### Understanding DDEV's Architecture

`Explain DDEV's project structure and architecture`

--

#### Advanced Navigation Techniques

**Start with the Entry Point:**  
`Show me the main() function and how DDEV processes commands`

This reveals `cmd/ddev/main.go` and the Cobra command structure.

--

**Follow the Data Flow:**  
`Trace the execution from 'ddev start' to container creation`

Response should show: `cmd/start.go` → `pkg/ddevapp/ddevapp.go` → Docker operations


---

### Strategic Code Discovery

#### Finding Implementation Details

**Command Implementation Pattern:**  
`Where is the ddev start command implemented?`

`cmd/ddev/cmd/start.go` → `pkg/ddevapp/ddevapp.Start()`

`Show me container lifecycle management`

`pkg/ddevapp/ddevapp.go` → Docker operations

--

#### Dependency Analysis

**System Relationships:**  

`Show me all packages that import dockerutil`

`Find functions that create Docker containers`

`Explain how configuration flows through the system`

`Map the relationship between DdevApp and container management`

--

#### Pattern Recognition

**DDEV Conventions:**  

`Show me DDEV's error handling patterns`

```go
// Standard DDEV error pattern:
if err := app.ValidateConfig(); err != nil {
    return fmt.Errorf("failed to validate config for %s: %w", app.Name, err)
}
```

`How does DDEV handle logging?`

```go
// DDEV logging pattern:
util.Debug("Starting containers for %s", app.Name)
util.Success("Successfully started %s", app.Name)
util.Failed("Failed to start %s: %v", app.Name, err)
```

💡 **Navigation Strategy:** Start with "Explain the architecture" then drill down to specific components

--

### Go Development Patterns

#### DDEV-Specific Architecture Patterns

**1. Command Pattern Implementation:**  

`Show me how DDEV implements the command pattern`

Every DDEV command follows this structure:

```go
func NewCmdStart() *cobra.Command {
    cmd := &cobra.Command{
        Use:   "start [projectname ...]",
        Short: "Start a ddev project.",
        Long:  `Start initializes and configures the web server and database containers...`,
        RunE:  cmdStart,
    }
    return cmd
}

func cmdStart(cmd *cobra.Command, args []string) error {
    // Command logic implementation
    // Always follows: validation → execution → error handling
}
```

--


🔧 **AI Development Tip:** Always ask Claude to "follow DDEV patterns" when generating new code

---

## Live Demonstrations

Note: Section 5 of 7 - Real-world application of Claude Code with DDEV

---

### Demo Overview

**Let's work on a real DDEV issue:**

Gitpod "classic" unfortunately is no more as of today, so can be removed from the codebase. 

**[Issue 6891](https://github.com/ddev/ddev/issues/6891)**

Explains about the process of removing it.


---

#### Prompt Claude to Explain the Issue

- Introduce Claude to [GitHub Issue #6891](https://github.com/ddev/ddev/issues/6891)

`Read https://github.com/ddev/ddev/issues/6891 and describe the problem in detail`

`Review the DDEV codebase and explain what things need to change to accomplish this. There are docs, Gitpod configuration files, and go code that adjusts for the use of Gitpod.`

`Make a plan to remove these items separately in a separate commit for each topic.`



---

#### Walk Claude through the process

Review each step. Consider letting claude continue without permissions on each item.

---


## Best Practices

Note: Section 6 of 7 - Guidelines for effective AI-assisted development

--

### Code Quality Principles

#### Core Guidelines for AI-Assisted Development

**🛡️ Respect Existing Test Coverage**
```go
// ❌ Don't do this: Modifying existing tests without clear justification
func TestExistingFunction(t *testing.T) {
    // Changed expected behavior without understanding impact
}

// ✅ Do this: Add new tests, preserve existing ones
func TestExistingFunction_NewScenario(t *testing.T) {
    // New test for additional functionality
}
```

--

**🔧 Leverage Static Analysis**
- **Use DDEV's existing tooling:** `make lint`, `make test`
- **Pre-commit hooks:** Let tools catch issues before review
- **Code formatting:** Run `gofmt` and follow Go conventions

--

**🏛️ Follow Project Conventions**
```go
// Ask Claude Code: "Make this function follow DDEV's conventions"
// Before: Inconsistent error handling
func badExample() error {
    return errors.New("something went wrong")
}

// After: DDEV-style error wrapping
func goodExample() error {
    return fmt.Errorf("failed to start app: %w", err)
}
```

--

### Testing Best Practices

#### AI-Powered Test Generation

**✨ AI is Great at Test Creation**
```go
// Prompt: "Generate comprehensive tests for this DDEV function"
func TestDdevApp_GetConfigPath(t *testing.T) {
    tests := []struct {
        name     string
        app      *DdevApp
        filename string
        want     string
    }{
        {
            name: "valid filename",
            app:  &DdevApp{AppConfDir: func() string { return "/app/.ddev" }},
            filename: "config.yaml",
            want: "/app/.ddev/config.yaml",
        },
        {
            name: "empty filename",
            app:  &DdevApp{AppConfDir: func() string { return "/app/.ddev" }},
            filename: "",
            want: "/app/.ddev",
        },
        // AI generates more edge cases...
    }
    // Test implementation...
}
```

--

**🔍 Review Generated Tests Carefully**
- **Verify assertions** make logical sense
- **Check edge cases** are actually edge cases  
- **Validate test data** represents real scenarios
- **Ensure tests fail** when they should
- **If you don't understand the test, it's not a great thing**

--

**🎯 Effective Test Generation Prompts**
- "Generate unit tests with edge cases for this function"
- "Create integration tests for DDEV container startup"
- "Add tests for error handling in this database function"

---

### Prompt Engineering

#### Crafting Effective Prompts for Development

**🎯 Be Specific About Requirements**

❌ **Vague:** "Fix this function"

✅ **Specific:** "Fix this function to handle MySQL 8.0 authentication, following DDEV's error handling patterns and including unit tests"

❌ **Unclear:** "Make this better"  

✅ **Clear:** "Refactor this function to use DDEV's logging utilities and improve error messages for users. Use the pattern found in..."

--

**📋 Provide Context About DDEV**

**🏗️ Structure Context:**
> "This is part of DDEV's container management system. DDEV uses docker-compose to orchestrate containers. Follow existing patterns in pkg/ddevapp for container lifecycle management."

---

**🧪 Testing Context:**
> "Generate tests following DDEV's testing patterns. Use testify/require, include both positive and negative test cases, and follow the existing test file structure in this directory."

--

**🔄 Iterate and Refine**

**1️⃣ First attempt:** "Add error handling to this function"

**2️⃣ Refined:** "Add DDEV-style error handling with proper error wrapping"

**3️⃣ Specific:** "Add error handling that wraps errors with context and uses DDEV's util.Error() for user-facing messages"

--

**💡 Proven DDEV Prompts**
- "Explain how this DDEV component works and its dependencies"
- "Generate comprehensive tests for this function including edge cases"
- "Refactor this code to follow DDEV's Go conventions and patterns"
- "Add proper documentation following DDEV's documentation style"

---

## Q&A & Resources

Note: Section 7 of 7 - Discussion and follow-up materials

--

### Key Takeaways

- **AI enhances** rather than replaces developer skills. It's like working at a higher level of abstraction.
- **Testing workflows** see the biggest immediate benefits
- **Incremental adoption** is the best approach

---

**📚 Resources & Follow-up**

**Essential Documentation:**
- **DDEV Docs:** [ddev.readthedocs.io](https://ddev.readthedocs.io)
- **Claude Code Docs:** [docs.anthropic.com/claude-code](https://docs.anthropic.com/claude-code)
- **DDEV GitHub:** [github.com/ddev/ddev](https://github.com/ddev/ddev)
- **Contact us:** [Contacts and Discord](https://ddev.com/contact/)

**Training Materials:**
- **Claude Code Class at Coursera:** [coursera.org/learn/claude-code](https://www.coursera.org/learn/claude-code)

---

### Thank You!

**Questions?**

**Randy Fay**  
DDEV Maintainer  
[GitHub: @rfay](https://github.com/rfay)

**Presentation Materials:**  
Available at: [GitHub Repository Link]

Note: End with contact information and availability for follow-up questions.
