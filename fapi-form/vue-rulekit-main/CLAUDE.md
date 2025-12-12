# Vue RuleKit

This repository contains Vue.js development best practices and instructions templates that users copy to their projects and give to AI Agents. It's NOT a standard Vue.js application.

ALWAYS communicate in a simple, straightforward manner, DO NOT hallucinate or treat the user as if they are always right.

## Repository Structure

- **HOME/**: Global Claude Code configurations and commands meant to be copied to user's home directory (`~/.claude/`)
- **PROJECT/**: Project-specific rules and configurations meant to be copied to Vue.js projects
  - Contains multiple `CLAUDE.md` files with specific guidance for components, composables, queries, stores, and pages
- **README.md**: Installation and setup instructions for users

## Key Files and Architecture

### Template Files Structure

```
HOME/
├── .claude/
│   ├── CLAUDE.md          # Global bash command aliases (ni, nb, t, nr, nun)
│   └── commands/
│       ├── optimize-images.md
│       └── new-command.md
│
PROJECT/
├── CLAUDE.md              # Project-level rules that are always applied
└── src/
    ├── components/CLAUDE.md   # Vue component best practices and patterns
    ├── composables/CLAUDE.md  # Composables patterns and examples
    ├── queries/CLAUDE.md      # (Empty - needs content)
    ├── stores/CLAUDE.md       # (Empty - needs content)
    └── pages/CLAUDE.md        # Routing patterns
```

## Common Tasks

Since this is a documentation repository, typical tasks involve:

- **Updating templates**: Modify CLAUDE.md files in PROJECT/ to improve Vue.js guidance
- **Adding new commands**: Create new .md files in HOME/.claude/commands/
- **Maintaining consistency**: Ensure all template files follow the same patterns and standards
- **Document changes**: Update README.md with any structural changes or new instructions

