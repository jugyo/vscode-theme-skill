# vscode-theme-skill

A Claude Code Skill that generates VSCode Color Themes and handles packaging and installation in one seamless workflow.

## Prerequisites

The following tools are required:

- [Node.js](https://nodejs.org/)
- [@vscode/vsce](https://github.com/microsoft/vscode-vsce) - `npm install -g @vscode/vsce`
- `code` CLI command - In VSCode: `Cmd+Shift+P` → "Shell Command: Install 'code' command in PATH"

## Installation

Clone and copy the skill to your Claude Code skills directory:

```bash
git clone https://github.com/jugyo/vscode-theme-skill.git
cp -r vscode-theme-skill/skills/vscode-theme ~/.claude/skills/
```

Reload Claude Code for automatic activation.

## Usage

Request theme creation in Claude Code like this:

```
"Create a blue-based dark VSCode theme"
"Make a Monokai-style VSCode theme"
"Create an eye-friendly light VSCode theme"
"I want to create a VSCode color theme"
```

The skill will automatically:

1. Check and verify required tools
2. Generate theme scaffolding
3. Design and configure the color palette
4. Package the extension
5. Install to VSCode

## Customization

After theme generation, you can provide feedback to adjust:

```
"Make the colors more subdued"
"Make the comment color darker"
"Change the accent color to red"
```

## File Structure

```
vscode-theme-skill/
├── .claude-plugin/
│   └── plugin.json
├── README.md
└── skills/
    └── vscode-theme/
        └── SKILL.md
```

## License

MIT
