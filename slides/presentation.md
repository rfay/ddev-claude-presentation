# DDEV Development with Claude Code
## Training Presentation

<img src="images/ddev-logo.svg" alt="DDEV Logo" class="ddev-logo">

**AI-Assisted Development Workflows**

---

**Presented by:** Randy Fay, DDEV Lead Maintainer  

🎯 **Goal:** Learn practical techniques for using Claude Code to enhance DDEV development workflows

---

## Table of Contents

<!-- Use smaller print for this slide -->
<span style="font-size: 0.85em">

1. **Introduction & Overview**
2. **Setup & Configuration**
3. **Technical Workflows**
4. **Live Demonstrations**
5. **Best Practices**
6. **Q&A & Resources**

</span>

---

**Start recording and captions:** Don't forget
**Navigation Tips:** Use arrow keys, 'o' for overview, 's' for speaker notes  
**Presenter Notes Available:** Press 's' to open speaker view with detailed timing and delivery guidance

---

## Introduction & Overview

Note: Section 1 of 6 - Setting the context for AI-assisted DDEV development

--

### What We'll Work At Today

**Practical AI-Assisted Development Techniques:**

* **Practical workflows** for DDEV development with Claude Code
* **Real-time implementation** of DDEV features and bug fixes
* **Best practices** for AI-assisted development in open source projects
* **Techniques applicable** to your own development projects

---

### About Claude Code

#### Capabilities

**Claude Code Capabilities:**
- **AI pair programming assistant** with deep code understanding
- **Context-aware analysis** of large codebases and complex architectures  
- **Conversation-based workflow** for iterative development
- **Multi-language expertise** with particularly strong Go, Python, and JavaScript support
- **Real-time assistance** for coding, debugging, testing, and documentation

--

#### Key Strengths

- **Pattern recognition** in existing codebases
- **Code generation** following established conventions
- **Test creation** with comprehensive edge case coverage
- **Documentation writing** in multiple formats
- **Debugging assistance** with error analysis and solutions

--

#### Current Limitations

- **Context windows** - works best with focused, specific tasks  
- **Knowledge cutoff** - may not know about very recent changes
- **Hallucination risk** - always verify generated code
- **Limited time usage**

--

🤖 **Key Principle:** Claude Code enhances human developers - it doesn't replace critical thinking and domain expertise

---

## Setup & Configuration

Note: Section 2 of 6 - Getting Claude Code ready for DDEV development

--

### Getting Started

- DDEV installed and working
- VS Code or JetBrains IDE (or no IDE at all)
- Git and GitHub CLI (optional but recommended)
- Claude Code installed and working 
- Claude Code/Anthropic account
- Basic Go knowledge helpful

---

## Technical Workflows

Note: Section 3 of 6 - Core development workflows with AI assistance

--

### Codebase Navigation

#### Understanding DDEV's Architecture

**Ask Claude Code:**  
> Explain DDEV's project structure and architecture

```
ddev/
├── cmd/ddev/                // Main CLI entry point and command definitions
│   ├── cmd/                 // Individual command implementations  
│   │   ├── start.go        // `ddev start` command
│   │   ├── config.go       // `ddev config` command
│   │   └── ...             // Other commands
├── pkg/                     // Core functionality packages
│   ├── ddevapp/            // Main application logic
│   ├── dockerutil/         // Docker operations
│   ├── globalconfig/       // Global configuration
│   └── util/               // Utility functions
├── containers/              // Docker container definitions
│   ├── ddev-webserver/     // Web server container
│   ├── ddev-dbserver/      // Database containers
│   └── ddev-router/        // Traefik router container
├── docs/                    // User and developer documentation
└── tests/                   // Test suites (Go unit tests + Bats integration tests)
```

--

#### Advanced Navigation Techniques

**Start with the Entry Point:**  
> Claude Code prompt: "Show me the main() function and how DDEV processes commands"  
This reveals `cmd/ddev/main.go` and the Cobra command structure.

--

**Follow the Data Flow:**  
> Claude Code prompt: "Trace the execution from 'ddev start' to container creation"  
Response should show: `cmd/start.go` → `pkg/ddevapp/ddevapp.go` → Docker operations

--

**Understanding Key Interfaces:**  
> Ask Claude Code: "Explain the Provider interface and its implementations"

```go
type Provider interface {
    GetType() string
    GetConfigPath() string  
    Validate() error
    // Shows how different hosting providers are abstracted
}
```

---

### Strategic Code Discovery

#### Finding Implementation Details

**Command Implementation Pattern:**  
> Where is the ddev start command implemented?  
`cmd/ddev/cmd/start.go` → `pkg/ddevapp/ddevapp.Start()`

> How does DDEV detect project type?  
`pkg/ddevapp/config.go` → `DetectAppType()` function

> Show me container lifecycle management  
`pkg/ddevapp/ddevapp.go` → Docker operations

--

#### Dependency Analysis

**System Relationships:**  
> Show me all packages that import dockerutil  
> Find functions that create Docker containers  
> Explain how configuration flows through the system  
> Map the relationship between DdevApp and container management

--

#### Pattern Recognition

**DDEV Conventions:**  
> Ask Claude Code: "Show me DDEV's error handling patterns"

```go
// Standard DDEV error pattern:
if err := app.ValidateConfig(); err != nil {
    return fmt.Errorf("failed to validate config for %s: %w", app.Name, err)
}
```

> Ask Claude Code: "How does DDEV handle logging consistently?"

```go
// DDEV logging pattern:
util.Debug("Starting containers for %s", app.Name)
util.Success("Successfully started %s", app.Name)
util.Failed("Failed to start %s: %v", app.Name, err)
```

💡 **Navigation Strategy:** Always start with "Explain the architecture" then drill down to specific components

--

### Go Development Patterns

#### DDEV-Specific Architecture Patterns

**1. Command Pattern Implementation:**  
> Ask Claude Code: "Show me how DDEV implements the command pattern"  
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

**2. Application State Management:**  
> Ask Claude Code: "Explain DDEV's application state pattern"

```go
type DdevApp struct {
    Name          string
    Type          string
    PHPVersion    string
    WebImage      string
    ConfigPath    string
    // State is immutable once created, modified through methods
}

// State transitions are explicit and validated
func (app *DdevApp) Start() error {
    if app.Status == ddevapp.SiteRunning {
        return fmt.Errorf("app %s is already running", app.Name)
    }
    // State change logic with validation
}
```

--

**3. Provider Pattern for Extensibility:**  
> Ask Claude Code: "How does DDEV use the provider pattern?"

```go
type Provider interface {
    GetType() string
    GetConfigPath() string
    Validate() error
    Write(configPath string) error
}

// Implementation for different hosting providers
type PlatformshProvider struct {
    app *DdevApp
}
func (p *PlatformshProvider) GetType() string { return "platform.sh" }
```

---

#### Error Handling Patterns
**DDEV's Consistent Error Strategy:**
```go
// Ask Claude Code: "Generate DDEV-style error handling for this function"

// Before: Basic error handling
func StartContainers() error {
    if err := dockerutil.ComposeUp(); err != nil {
        return err
    }
}

// After: DDEV-style error handling with context
func (app *DdevApp) StartContainers() error {
    util.Debug("Starting containers for project %s", app.Name)
    
    if err := app.ValidateContainerConfig(); err != nil {
        return fmt.Errorf("container configuration invalid for %s: %w", app.Name, err)
    }
    
    if err := dockerutil.ComposeUp(app.GetComposeFiles()...); err != nil {
        return fmt.Errorf("failed to start containers for %s: %w", app.Name, err)
    }
    
    util.Success("Containers started successfully for %s", app.Name)
    return nil
}
```

🔧 **AI Development Tip:** Always ask Claude to "follow DDEV patterns" when generating new code

--

### Let's Try It Out!

---

## Live Demonstrations

Note: Section 4 of 6 - Working through real GitHub issues

--

### Demo Overview

**Three real DDEV issues:**

1. **Issue #7424:** [FrankenPHP launch error](https://github.com/ddev/ddev/issues/7424)
2. **Issue #5337:** [Add-on dependency management](https://github.com/ddev/ddev/issues/5337)
3. **Issue #7537:** [Xdebug host resolution](https://github.com/ddev/ddev/issues/7537)

**Each demo shows:** Problem analysis → Solution design → Implementation → Testing

--

### Demo 1: FrankenPHP `ddev launch` problem, Issue #7424

#### Step 1: Prompt Claude to Explain the Issue

- Introduce Claude to [GitHub Issue #7424](https://github.com/ddev/ddev/issues/7424)

`Read https://github.com/ddev/ddev/issues/7424 and explain the problem with `ddev launch` and FrankenPHP.`

--

#### Step 2: Reproduce the Bug

Prompt to Claude:  
`How can I reproduce the bug described in https://github.com/ddev/ddev/issues/7424 using a fresh DDEV project and the FrankenPHP add-on?`

--

#### Step 3: Analyze and Identify the Root Cause

- Analyze the error message from the failed launch
- Ask Claude to read and explain the launch command code (a bash custom command)
- Prompt:  
  > "Analyze the error output and the launch custom command. What is causing the failure with FrankenPHP?"

--

#### Step 4: Implement and Test the Fix

- Ask Claude to suggest a fix based on the analysis and the issue discussion
- Implement the fix as suggested
- Test the solution to confirm the bug is resolved
- Prompt:  
  > "Propose and explain a fix for the FrankenPHP launch issue, and describe how to test it."

--

### Demo 2: Add-on Dependencies
#### GitHub Issue #5337

**Problem:** Allow add-ons to download other add-ons as dependencies

**AI-Assisted Approach:**
- Analyze existing add-on system
- Design dependency resolution
- Implement recursive installation
- Create comprehensive tests

Note: This demonstrates AI-assisted feature development from conception to completion.

--

### Demo 3: Xdebug Enhancement
#### GitHub Issue #7537

**Problem:** Better `host.docker.internal` handling for Xdebug

**AI-Assisted Approach:**
- Understand container networking
- Research cross-platform solutions
- Implement improved detection
- Test across environments

Note: This demonstrates AI assistance with complex system-level programming.

---

## Best Practices

Note: Section 5 of 6 - Guidelines for effective AI-assisted development

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

**✨ AI Excels at Test Creation**
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
```
❌ Vague: "Fix this function"
✅ Specific: "Fix this function to handle MySQL 8.0 authentication, 
   following DDEV's error handling patterns and including unit tests"

❌ Unclear: "Make this better"  
✅ Clear: "Refactor this function to use DDEV's logging utilities 
   and improve error messages for users". Use the pattern found in ...
```

--

**📋 Provide Context About DDEV**
```
🏗️ Structure Context:
"This is part of DDEV's container management system. DDEV uses 
docker-compose to orchestrate containers. Follow existing patterns 
in pkg/ddevapp for container lifecycle management."

🧪 Testing Context:
"Generate tests following DDEV's testing patterns. Use testify/require, 
include both positive and negative test cases, and follow the existing 
test file structure in this directory."
```

--

**🔄 Iterate and Refine**
```
1️⃣ First attempt: "Add error handling to this function"
2️⃣ Refined: "Add DDEV-style error handling with proper error wrapping"
3️⃣ Specific: "Add error handling that wraps errors with context and 
    uses DDEV's util.Error() for user-facing messages"
```

--

**💡 Proven DDEV Prompts**
- "Explain how this DDEV component works and its dependencies"
- "Generate comprehensive tests for this function including edge cases"
- "Refactor this code to follow DDEV's Go conventions and patterns"
- "Add proper documentation following DDEV's documentation style"

---

## Q&A & Resources

Note: Section 6 of 6 - Questions, answers, and follow-up resources

--

### Key Takeaways

- **AI enhances** rather than replaces developer skills. It's like working at a higher level of abstraction.
- **Testing workflows** see the biggest immediate benefits
- **Incremental adoption** is the best approach

---

### Exercise Materials & Templates

**1. Navigation Deep Dive (30 minutes)**
- Explore DDEV's testing framework architecture
- Practice with different types of DDEV providers
- Map out the database service implementation

--

**2. Advanced Code Review (45 minutes)**
- Review a complete pull request with Claude Code
- Compare AI suggestions with actual DDEV maintainer feedback
- Practice the full review cycle: analysis → suggestions → improvement

--

**3. Real Issue Practice (60 minutes)**
- Choose an interesting DDEV GitHub issue
- Work through the complete development cycle
- Submit your solution approach for community feedback

--

**📚 Resources & Follow-up**

**Essential Documentation:**
- **DDEV Documentation:** [ddev.readthedocs.io](https://ddev.readthedocs.io)
- **Claude Code Docs:** [docs.anthropic.com/claude-code](https://docs.anthropic.com/claude-code)
- **DDEV GitHub:** [github.com/ddev/ddev](https://github.com/ddev/ddev)
- **Community Slack:** [ddev.com/slack](https://ddev.com/slack)

--

**Advanced Learning:**
- **DDEV Architecture Guide:** Understanding the codebase structure
- **Go Development Patterns:** Best practices for Go development
- **AI-Assisted Development Blog:** [blog.ddev.com/ai-development](https://blog.ddev.com)
- **Monthly DDEV Office Hours:** Ask questions and share experiences

--

**Community Resources:**
- **DDEV Contributor Guide:** Step-by-step contribution process
- **AI Development Discussion:** Join the #ai-tools channel in DDEV Slack
- **Office Hours Calendar:** [ddev.com/events](https://ddev.com/events)

Note: Provide comprehensive resources for continued learning. Mention that exercise materials will be made available after the presentation.

--

### Thank You!

**Questions?**

**Randy Fay**  
DDEV Maintainer  
[GitHub: @rfay](https://github.com/rfay)

**Presentation Materials:**  
Available at: [GitHub Repository Link]

Note: End with contact information and availability for follow-up questions.
