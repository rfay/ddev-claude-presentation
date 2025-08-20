# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Communication Style

- Use direct, concise language without unnecessary adjectives or adverbs
- Avoid flowery or marketing-style language ("tremendous", "dramatically", "revolutionary", etc.)
- Don't include flattery or excessive praise ("excellent!", "perfect!", "great job!")
- State facts and findings directly without embellishment
- Skip introductory phrases like "I'm excited to", "I'd be happy to", "Let me dive into"

## Project Overview

This repository contains materials for a DDEV Claude presentation, demonstrating the integration and capabilities of Claude Code with DDEV development workflows.

## Development Notes

### Branch Naming

Use descriptive branch names that include:
- Date in YYYYMMDD format
- Your GitHub username  
- Brief description of the work

Format: `YYYYMMDD_<username>_<short_description>`

### Branch Creation Strategy

```bash
git fetch upstream && git checkout -b <branch_name> upstream/main --no-track
```

## Important Instruction Reminders

Do what has been asked; nothing more, nothing less.
NEVER create files unless they're absolutely necessary for achieving your goal.
ALWAYS prefer editing an existing file to creating a new one.
NEVER proactively create documentation files (*.md) or README files. Only create documentation files if explicitly requested by the User.

## Task Master AI Instructions
**Import Task Master's development workflow commands and guidelines, treat as if import is in the main CLAUDE.md file.**
@./.taskmaster/CLAUDE.md
