# Vue.js RuleKit

> Vibe code Vue applications with confidence 🧑‍💻

## Installation

For an optimal experience, please follow the steps below to set up Vue RuleKit in your project.

1. [Setup](#setup)
2. [Initialize the project](#initialize-the-project)
3. [Recommended tools](#recommended-tools)

### Setup

- `./HOME` contains files that can be added globally (to user settings) like Claude Code commands. It refers to `~/` or `$HOME`.
- `./PROJECT` contains files that can be copied to your project, like rules.

To keep things simple and adaptable, you have **direct access to all the markdown files**. You should copy the rules to your project and adapt them as needed.

#### Copying the rules

Directly copy the `PROJECT/*` files to your project:

```bash
cp -r PROJECT/* ~/my-project/
```

This assumes you have the same folder structure as the repository. Adapt the files after copying if needed, **you can even ask Claude/Cursor/Copilot to move them for you**. Depending on what's your agent, you can delete other files.

- Claude Code: keep `.claude/` and `CLAUDE.md` files
- Others IDE (Cursor, VSCode Copilot): use the [instructions](#other-agents) below
- Other agents: Rename `CLAUDE.md` to `AGENTS.md`

> [!TIP]
> **Fill the name and description** of your project in the root `CLAUDE.md`/`AGENTS.md` file. This is something you _have to do_ and it's better if you do it manually. Depending on your team's workflow, add any project-specific workflow like creating PRs, using a specific MCP server, etc.

Copy global commands too, see inside `HOME/README.md` and follow the instructions there.

<details>
  <summary>
    <h4>Linking the rules</h4>
  </summary>

**Not recommended except for testing purposes.**

This version allows you to:

- 👍 Modify the rules directly in your project
- 👍 Applies to all projects that link the rules
- 👍 Keep the rules updated automatically by running `git pull` in vue-rulekit

But has some limitations:

- 👎 If the format of rules for agents evolve, updating the repository may break your agent workflow
- 👎 All team members need to have the same linked folder
- 👎 Requires absolute paths for symbolic links
- 👎 Cannot be committed to git

If you compare it to copying:

- 👍 Modify the rules directly in your project
- 👍 Share them with your teammates who **also purchased RuleKit**
- 👍 Copy with one single command
- 👎 You need to copy the rules to each project
- 👎 You need to keep the rules updated manually each time you update RuleKit

It's much safer to just copy the files and move them to match your project structure.

```bash
cd ~/my-project
ln -s <absolute-path-to-vue-rulekit>/PROJECT/.claude ~/my-project/.claude
```

Example:

If I want to add the rules to a project called `rulekit-landing` in my home directory (`~/`) and I have cloned _vue-rulekit_ in my home directory, I would do the following:

```bash
ln -s ~/vue-rulekit/PROJECT/.claude ~/rulekit-landing/.claude
```

</details>

### Other agents

<details>
  <summary>
    <h4>Copilot</h4>
  </summary>

For Copilot, you need to copy the files according to the [Copilot documentation](https://code.visualstudio.com/docs/copilot/copilot-customization). Use this automated script to set up all instruction files with proper frontmatter and structure:

```bash
# Set path to vue-rulekit (adjust this path to where you cloned vue-rulekit)
RULEKIT_PATH="$HOME/vue-rulekit"

# Create .github/instructions directory structure
mkdir -p .github/instructions

# Copy main project rules (no frontmatter needed for main instructions)
cp "$RULEKIT_PATH/PROJECT/CLAUDE.md" .github/copilot-instructions.md

# Auto-discover and copy all domain-specific CLAUDE.md files
find "$RULEKIT_PATH/PROJECT/src" -name "CLAUDE.md" | while read -r file; do
  # Extract directory name (components, composables, pages, etc.)
  dir_name=$(basename "$(dirname "$file")")

  # Create appropriate instruction file with frontmatter
  cat > ".github/instructions/vue-${dir_name}.md" << EOF
---
description: Vue.js ${dir_name} patterns and best practices
applyTo: "**/${dir_name}/**/*"
---
$(cat "$file")
EOF
done
```

**Setup steps:**

1. Adjust `RULEKIT_PATH` to point to where you cloned this repository
2. Run the script from your project root directory
3. Edit `.github/copilot-instructions.md` to add your project name and description

The script automatically creates instruction files with proper frontmatter for all Vue.js domains and uses `applyTo` patterns for targeted application.

**Note:** Based on testing (29/07/2025), VS Code doesn't automatically include relevant instructions based on `applyTo`, so you may need to manually reference specific instruction files in Copilot chat using `#` when needed.

</details>

<details>
  <summary>
    <h4>Cursor</h4>
  </summary>

For Cursor, use this automated script to set up all rules with proper frontmatter and file structure:

```bash
# Set path to vue-rulekit (adjust this path to where you cloned vue-rulekit)
RULEKIT_PATH="$HOME/vue-rulekit"

# Create .cursor directory structure
mkdir -p .cursor/rules

# Copy main project rules
cat > .cursor/rules/global.mdc << EOF
---
description: Vue.js project rules and standards
alwaysApply: true
---
$(cat "$RULEKIT_PATH/PROJECT/CLAUDE.md")
EOF

# Auto-discover and copy all domain-specific CLAUDE.md files
find "$RULEKIT_PATH/PROJECT/src" -name "CLAUDE.md" | while read -r file; do
  # Extract directory name (components, composables, pages, etc.)
  dir_name=$(basename "$(dirname "$file")")

  # Create appropriate .mdc file with frontmatter
  cat > ".cursor/rules/vue-${dir_name}.mdc" << EOF
---
description: Vue.js ${dir_name} patterns and best practices
globs: ["**/${dir_name}/**/*"]
alwaysApply: false
---
$(cat "$file")
EOF
done
```

**Setup steps:**

1. Adjust `RULEKIT_PATH` to point to where you cloned this repository
2. Run the script from your project root directory
3. Edit `.cursor/rules/global.mdc` to add your project name and description

The script automatically creates `.mdc` files with proper frontmatter for all Vue.js domains and uses glob patterns for smart rule application.

</details>

## Initialize the project

This step is very important, take the time to read the instructions files and **adapt them to your project**. Add a title relevant to your project, a description, specific instructions, etc.

You can ask an LLM to generate it and it will do it just fine with twice the amount of words. So if you do, make sure to review the generated content and **remove redundant information**.

## Recommended tools

Here are some recommended tools that might be used by the rules.

### Command line tools

- [`magick` (previously `convert`)](https://imagemagick.org/) - For image manipulation `brew install imagemagick`
- [`cwebp`](https://developers.google.com/speed/webp) - For WebP image format `brew install webp`

### MCP servers

Add the following MCP servers globally so they can be used in all your projects:

- **Playwright**: Browser automation for visual testing and UI interactions

  ```sh
  # claude code
  claude mcp add --scope user 'playwright' npx @playwright/mcp@latest
  ```

See [documentation](https://docs.anthropic.com/en/docs/claude-code/mcp) for more information.

## Resources

Here are some resources I recommend you to check out **and fully read** (no AI summaries, please):

- [Claude best practices](https://www.anthropic.com/engineering/claude-code-best-practices): This will give you a good understanding on how to organize rules for Claude Code, how to add custom commands, and how to improve your prompts.
- Use `/clear` often, the larger the context, the more likely agents will hallucinate or stop following the rules. **Split your tasks into smaller ones** to get better results.

## Roadmap

- [x] Vue Components best practices
- [ ] Composables Best practices
- [x] Vue Router + file based routing best practices
- [x] Support for Cursor
- [ ] Pinia Colada best practices
- [ ] Nuxt Best Practices
- [x] Testing Components best practices
- [ ] VueUse most used composables
