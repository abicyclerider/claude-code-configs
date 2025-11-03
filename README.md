# Claude Code Configurations

A collection of reusable slash commands and CLAUDE.md templates for Claude Code, designed to enhance your AI-assisted coding workflow.

## Repository Structure

```
claude-code-configs/
├── commands/           # Slash commands for Claude Code
│   └── teach.md       # Interactive coding tutor command
├── templates/         # CLAUDE.md templates for different project types
│   └── CLAUDE_LEARNING.md  # Template for learning/tutorial projects
└── README.md
```

## Available Commands

### `/teach` - Interactive Coding Tutor

Activates an interactive teaching mode where Claude acts as a coding tutor who:
- Coaches you to write code yourself rather than writing it for you
- Asks you to predict outcomes before running code
- Quizzes you on understanding with targeted questions
- Provides progressive hints instead of full solutions
- Celebrates your progress and correct answers
- Guides you step-by-step through concepts

**Usage**: Type `/teach` in any Claude Code conversation to activate tutor mode.

## Available Templates

### CLAUDE_LEARNING.md

A CLAUDE.md template for learning and tutorial projects that instructs Claude to use the interactive teaching approach automatically.

**Usage**: Copy this template to your learning project as `.claude/CLAUDE.md` and customize the learning goals section.

## Setup Instructions

### Prerequisites

- Claude Code installed and configured
- Git installed on your system

### Installation

1. **Clone this repository**:
   ```bash
   cd ~/repos  # or your preferred location
   git clone <your-repo-url> claude-code-configs
   cd claude-code-configs
   ```

2. **Set up symlinks** to make commands available in Claude Code:
   ```bash
   # Create the .claude/commands directory if it doesn't exist
   mkdir -p ~/.claude/commands

   # Symlink individual commands
   ln -s ~/repos/claude-code-configs/commands/teach.md ~/.claude/commands/teach.md

   # Or symlink the entire commands directory (alternative approach)
   # ln -s ~/repos/claude-code-configs/commands/* ~/.claude/commands/
   ```

3. **Verify installation**:
   - Open Claude Code
   - Type `/` to see available commands
   - You should see `/teach` in the list

### Using Templates

To use a template in your project:

1. Create a `.claude` directory in your project root (if it doesn't exist):
   ```bash
   mkdir -p .claude
   ```

2. Copy the desired template:
   ```bash
   cp ~/repos/claude-code-configs/templates/CLAUDE_LEARNING.md .claude/CLAUDE.md
   ```

3. Customize the template with your project-specific learning goals

## Adding More Commands

To add your own commands to this repository:

1. Create a new `.md` file in the `commands/` directory
2. Write your command prompt (see [Claude Code documentation](https://docs.claude.com) for syntax)
3. Symlink it to `~/.claude/commands/`:
   ```bash
   ln -s ~/repos/claude-code-configs/commands/your-command.md ~/.claude/commands/your-command.md
   ```
4. Commit and push to share with others

## Contributing

Feel free to fork this repository and add your own useful commands and templates! Pull requests are welcome.

## Tips

- **Version control**: Since these configs are in git, you can track changes and share improvements
- **Sync across machines**: Clone this repo on multiple machines and symlink to keep your commands in sync
- **Backup**: Your commands and templates are safely backed up in git
- **Collaboration**: Share useful commands with your team via GitHub

## License

[Choose an appropriate license - MIT, Apache 2.0, etc.]

## Resources

- [Claude Code Documentation](https://docs.claude.com/claude-code)
- [Slash Commands Guide](https://docs.claude.com/claude-code/slash-commands)
- [CLAUDE.md Guide](https://docs.claude.com/claude-code/claude-md)
