# Live Demo Environment Setup

This directory contains setup instructions and materials for the live demonstrations during the DDEV + Claude Code presentation.

## Prerequisites

- **DDEV installed** and working on your system
- **Claude Code** properly configured in your IDE
- **Git** with appropriate credentials for GitHub
- **Go development environment** (Go 1.19+ recommended)
- **Make** build tools

## Demo Environment Setup

### 1. Clone DDEV Repository

```bash
# Clone in a demo-specific directory to avoid conflicts
git clone https://github.com/ddev/ddev.git ddev-demo
cd ddev-demo

# Verify the environment
make setup
make test  # This may take a while - run beforehand
```

### 2. Configure IDE for Presentation

**VS Code Settings for Demo:**
```json
{
    "editor.fontSize": 16,
    "editor.fontFamily": "Monaco, 'Courier New', monospace",
    "terminal.integrated.fontSize": 16,
    "workbench.colorTheme": "Default High Contrast",
    "editor.minimap.enabled": false,
    "editor.lineNumbers": "on",
    "editor.renderWhitespace": "boundary"
}
```

**JetBrains Settings:**
- Font size: 16pt minimum
- Theme: High contrast or Darcula
- Disable distractions: Turn off tool windows, minimap
- Enable line numbers and whitespace visualization

### 3. Prepare Demo Branches

```bash
# Create branches for each demo
git checkout -b demo/addon-dependencies
git push -u origin demo/addon-dependencies

git checkout main
git checkout -b demo/frankenphp-launch  
git push -u origin demo/frankenphp-launch

git checkout main
git checkout -b demo/xdebug-host-resolution
git push -u origin demo/xdebug-host-resolution

# Return to main for starting point
git checkout main
```

### 4. Test Claude Code Integration

Verify Claude Code works with the DDEV codebase:

```bash
# Test queries to validate setup:
# 1. "Explain the structure of the DDEV codebase"
# 2. "Show me how the ddev start command is implemented"
# 3. "Generate a simple test for the DdevApp struct"
```

## Demo Scenarios

### Demo 1: Issue #5337 - Add-on Dependencies
**Location:** `pkg/ddevapp/` 
**Focus:** Implementing dependency management for DDEV add-ons
**Key Files:**
- `pkg/ddevapp/addons.go`
- `pkg/ddevapp/config.go`

### Demo 2: Issue #7424 - FrankenPHP Launch Error  
**Location:** `cmd/ddev/cmd/`
**Focus:** Debugging and fixing launch command issues
**Key Files:**
- `cmd/ddev/cmd/launch.go`
- `pkg/ddevapp/launch.go`

### Demo 3: Issue #7537 - Xdebug Host Resolution
**Location:** `pkg/ddevapp/`
**Focus:** Improving container networking for debugging
**Key Files:**
- `pkg/ddevapp/docker.go`
- `pkg/ddevapp/config.go`

## Presentation Setup Checklist

### Before the Presentation
- [ ] Clone DDEV repository in demo directory
- [ ] Run `make setup` and `make test` successfully
- [ ] Configure IDE with presentation-friendly settings
- [ ] Test Claude Code with DDEV codebase
- [ ] Create and test all demo branches
- [ ] Prepare backup recordings of each demo
- [ ] Test screen sharing in Zoom with sample content

### During Presentation Setup (10 minutes before)
- [ ] Open IDE with DDEV project loaded
- [ ] Start screen sharing and verify visibility
- [ ] Test Claude Code with a simple query
- [ ] Have backup materials readily accessible
- [ ] Ensure stable internet connection
- [ ] Close unnecessary applications

### Demo Flow Structure
Each demo follows this pattern:
1. **Explain the GitHub issue** (2 minutes)
2. **Show the current state** (1 minute)  
3. **Use Claude Code to analyze** (2 minutes)
4. **Implement solution with AI assistance** (3 minutes)
5. **Test and validate** (2 minutes)
6. **Q&A and discussion** (2 minutes)

## Troubleshooting

### Common Issues
- **Claude Code not responding:** Check API key and network
- **Build failures:** Ensure Go environment is properly configured  
- **Git branch issues:** Use backup branches or reset to known state
- **Screen sharing problems:** Have backup slides ready

### Fallback Options
- Pre-recorded demo videos in `demo-setup/recordings/`
- Screenshots of key steps in `demo-setup/screenshots/`
- Code snippets for manual typing in `demo-setup/snippets/`

## Post-Demo Cleanup

```bash
# Clean up demo branches if needed
git branch -d demo/addon-dependencies
git branch -d demo/frankenphp-launch
git branch -d demo/xdebug-host-resolution

# Or keep them for audience reference
git tag demo-session-2025-08-21
```