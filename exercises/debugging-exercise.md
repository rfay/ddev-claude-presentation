# DDEV Debugging Exercise - Missing Cobra Command

## Objective
Practice systematic debugging with Claude Code using a common DDEV development issue.

## The Problem
You're implementing a new DDEV command, but it's not appearing in the CLI help output. This is a real scenario that new DDEV contributors often encounter.

## Broken Code
```go
// This command isn't showing up in 'ddev help'
var NewFeatureCmd = &cobra.Command{
    Use:   "newfeature",
    Short: "Adds a new feature to DDEV",
    Run: func(cmd *cobra.Command, args []string) {
        fmt.Println("New feature running!")
    },
}

func init() {
    RootCmd.AddCommand(NewFeatureCmd)
}
```

## Exercise Steps

### Step 1: Problem Analysis
1. Ask Claude: "Why isn't this cobra command appearing in DDEV help?"
2. Have Claude explain the most likely causes
3. Ask for a systematic debugging approach

### Step 2: Investigation
1. Ask Claude: "Show me how DDEV typically registers new commands"
2. Follow up: "How do existing DDEV commands differ from this implementation?"
3. Request specific examples from the DDEV codebase

### Step 3: Solution
1. Ask Claude to provide the corrected code
2. Have Claude explain the root cause and prevention
3. Validate the solution by comparing with real DDEV commands

## Common Debugging Prompts
```
"Analyze this error and suggest debugging steps"
"Compare this code to working examples in the codebase"
"What are the most likely causes of this issue?"
"Walk me through debugging this step by step"
"Show me the correct way to register commands in DDEV"
```

## The Root Issues (Spoiler Alert)
The typical problems include:
1. **Package imports:** Missing required imports
2. **Initialization order:** Commands registered before package is imported
3. **File location:** Command not in the expected directory structure
4. **Import cycles:** Creating circular dependencies
5. **Build tags:** Command not included in the build

## Expected Solution Elements
- Proper package structure following DDEV conventions
- Correct import statements
- Proper initialization order
- Understanding of cobra command hierarchy
- Knowledge of DDEV's command organization

## Success Criteria
- You can identify the root cause systematically
- You understand DDEV's command registration patterns
- You can fix similar issues in the future
- You've practiced AI-assisted debugging techniques

## Time Estimate
10 minutes during presentation, 30 minutes for extended practice

## Real-World Application
This debugging pattern applies to:
- Adding new DDEV commands and subcommands
- Understanding Go package structure
- Working with cobra CLI framework
- Contributing to DDEV development

## Extension Activities
1. Try adding a subcommand to an existing DDEV command
2. Implement command-line flags and options
3. Add proper help text and examples
4. Create tests for your new command

## Common Variations
- Command appears but arguments don't work
- Command works locally but not in built binary
- Command conflicts with existing commands
- Command missing from help but executes correctly