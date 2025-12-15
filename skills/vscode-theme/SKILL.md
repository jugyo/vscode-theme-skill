---
name: vscode-theme
description: Generate VSCode color themes, package them as .vsix files, and install to VSCode. Use when creating custom VSCode themes, designing color schemes, or when the user mentions VSCode theme, color theme, dark theme, or light theme.
---

# VSCode Theme Generator

Generate custom VSCode color themes from scratch, package them, and install them directly to VSCode.

## Prerequisites

The following tools are required:
- `@vscode/vsce` (VSCode Extension Manager)
- `code` command (VSCode CLI)

Check if tools are installed:
```bash
which vsce || echo "vsce is not installed"
which code || echo "code command is not installed"
```

Install if missing:
```bash
# vsce
npm install -g @vscode/vsce

# code command: In VSCode, press Cmd+Shift+P → "Shell Command: Install 'code' command in PATH"
```

## Instructions

### Step 1: Gather theme requirements

Ask the user for:
- Theme name (e.g., "Ocean Blue")
- Theme type: dark (`vs-dark`) or light (`vs`)
- Color preferences (base colors, accent colors)
- Any specific style inspiration

### Step 2: Create theme directory and files

Create the theme directory structure manually (no interactive prompts):

```bash
mkdir -p /tmp/<theme-id>/themes
```

Replace placeholders:
- `<theme-id>`: lowercase with hyphens (e.g., `ocean-blue-theme`)
- `<Theme Name>`: display name (e.g., `Ocean Blue Theme`)

### Step 3: Create package.json

Create `/tmp/<theme-id>/package.json`:

```json
{
  "name": "<theme-id>",
  "displayName": "<Theme Name>",
  "description": "<Theme description>",
  "version": "0.0.1",
  "publisher": "custom",
  "engines": {
    "vscode": "^1.74.0"
  },
  "categories": [
    "Themes"
  ],
  "contributes": {
    "themes": [
      {
        "label": "<Theme Name>",
        "uiTheme": "vs-dark",
        "path": "./themes/<theme-id>-color-theme.json"
      }
    ]
  }
}
```

Note: Set `"uiTheme": "vs"` for light themes.

### Step 4: Create the color theme file

Create `/tmp/<theme-id>/themes/<theme-id>-color-theme.json`:

```json
{
  "name": "<Theme Name>",
  "type": "dark",
  "colors": {
    "editor.background": "#1a1a2e",
    "editor.foreground": "#eaeaea",
    "activityBar.background": "#16213e",
    "activityBar.foreground": "#e94560",
    "activityBarBadge.background": "#e94560",
    "activityBarBadge.foreground": "#ffffff",
    "sideBar.background": "#1a1a2e",
    "sideBar.foreground": "#eaeaea",
    "sideBarTitle.foreground": "#eaeaea",
    "statusBar.background": "#0f3460",
    "statusBar.foreground": "#eaeaea",
    "statusBar.debuggingBackground": "#e94560",
    "titleBar.activeBackground": "#16213e",
    "titleBar.activeForeground": "#eaeaea",
    "titleBar.inactiveBackground": "#16213e",
    "titleBar.inactiveForeground": "#8a8a8a",
    "tab.activeBackground": "#1a1a2e",
    "tab.activeForeground": "#eaeaea",
    "tab.inactiveBackground": "#16213e",
    "tab.inactiveForeground": "#8a8a8a",
    "tab.border": "#16213e",
    "editorLineNumber.foreground": "#4a4a6a",
    "editorLineNumber.activeForeground": "#eaeaea",
    "editorCursor.foreground": "#e94560",
    "editor.selectionBackground": "#0f346080",
    "editor.wordHighlightBackground": "#0f346040",
    "editorBracketMatch.background": "#0f346060",
    "editorBracketMatch.border": "#e94560",
    "list.activeSelectionBackground": "#0f3460",
    "list.activeSelectionForeground": "#eaeaea",
    "list.hoverBackground": "#16213e",
    "input.background": "#16213e",
    "input.foreground": "#eaeaea",
    "input.border": "#0f3460",
    "focusBorder": "#e94560",
    "button.background": "#e94560",
    "button.foreground": "#ffffff",
    "button.hoverBackground": "#ff6b6b",
    "terminal.background": "#1a1a2e",
    "terminal.foreground": "#eaeaea"
  },
  "tokenColors": [
    {
      "scope": ["comment", "punctuation.definition.comment"],
      "settings": {
        "foreground": "#6a6a8a",
        "fontStyle": "italic"
      }
    },
    {
      "scope": ["string", "string.quoted"],
      "settings": {
        "foreground": "#98c379"
      }
    },
    {
      "scope": ["constant.numeric", "constant.language"],
      "settings": {
        "foreground": "#d19a66"
      }
    },
    {
      "scope": ["keyword", "storage.type", "storage.modifier"],
      "settings": {
        "foreground": "#c678dd"
      }
    },
    {
      "scope": ["entity.name.function", "support.function"],
      "settings": {
        "foreground": "#61afef"
      }
    },
    {
      "scope": ["entity.name.type", "entity.name.class", "support.class"],
      "settings": {
        "foreground": "#e5c07b"
      }
    },
    {
      "scope": ["variable", "variable.other"],
      "settings": {
        "foreground": "#e06c75"
      }
    },
    {
      "scope": ["entity.name.tag"],
      "settings": {
        "foreground": "#e06c75"
      }
    },
    {
      "scope": ["entity.other.attribute-name"],
      "settings": {
        "foreground": "#d19a66"
      }
    },
    {
      "scope": ["support.type.property-name"],
      "settings": {
        "foreground": "#61afef"
      }
    },
    {
      "scope": ["punctuation"],
      "settings": {
        "foreground": "#abb2bf"
      }
    },
    {
      "scope": ["meta.brace"],
      "settings": {
        "foreground": "#abb2bf"
      }
    }
  ]
}
```

Note: Set `"type": "light"` for light themes.

### Step 5: Package and install the theme

**For new themes:**

```bash
cd /tmp/<theme-id>
vsce package
code --install-extension /tmp/<theme-id>/<theme-id>-0.0.1.vsix
```

**For theme updates (IMPORTANT):**

When updating an existing theme, you must uninstall the old version first, then reinstall:

```bash
cd /tmp/<theme-id>
vsce package
code --uninstall-extension custom.<theme-id>
code --install-extension /tmp/<theme-id>/<theme-id>-0.0.1.vsix
```

The extension ID format is `<publisher>.<theme-id>` (e.g., `custom.ocean-blue-theme`).

Alternatively, bump the version in `package.json` before packaging:
```bash
# Update version in package.json (e.g., 0.0.1 -> 0.0.2)
cd /tmp/<theme-id>
vsce package
code --install-extension /tmp/<theme-id>/<theme-id>-<new-version>.vsix
```

### Step 6: Notify user

After installation:
> Theme installed successfully!
> Press `Cmd+K Cmd+T` (Mac) or `Ctrl+K Ctrl+T` (Windows/Linux) to select your new theme.

## Color Design Tips

### Dark themes
- Background: `#1a1a2e` to `#2d2d44`
- Foreground: `#d4d4d4` to `#eaeaea`
- Limit accent colors to 1-2

### Light themes
- Background: `#ffffff` to `#f5f5f5`
- Foreground: `#1a1a1a` to `#333333`
- Use muted accent colors

Example light theme colors:
```json
{
  "colors": {
    "editor.background": "#ffffff",
    "editor.foreground": "#1a1a1a",
    "activityBar.background": "#f0f0f0",
    "activityBar.foreground": "#0066cc",
    "sideBar.background": "#f5f5f5",
    "sideBar.foreground": "#333333",
    "statusBar.background": "#0066cc",
    "statusBar.foreground": "#ffffff",
    "titleBar.activeBackground": "#e8e8e8",
    "titleBar.activeForeground": "#333333",
    "tab.activeBackground": "#ffffff",
    "tab.inactiveBackground": "#ececec",
    "editorLineNumber.foreground": "#999999",
    "editorCursor.foreground": "#0066cc"
  },
  "tokenColors": [
    { "scope": "comment", "settings": { "foreground": "#6a9955", "fontStyle": "italic" } },
    { "scope": "string", "settings": { "foreground": "#a31515" } },
    { "scope": "constant.numeric", "settings": { "foreground": "#098658" } },
    { "scope": "keyword", "settings": { "foreground": "#0000ff" } },
    { "scope": "entity.name.function", "settings": { "foreground": "#795e26" } },
    { "scope": "entity.name.type", "settings": { "foreground": "#267f99" } },
    { "scope": "variable", "settings": { "foreground": "#001080" } }
  ]
}
```

### Accessibility
- Maintain contrast ratio of 4.5:1 or higher for text
- Test with colorblind simulation tools

## Troubleshooting

### `code` command not found
In VSCode: `Cmd+Shift+P` → `Shell Command: Install 'code' command in PATH`

### Theme not appearing
1. Restart VSCode
2. Run `Developer: Reload Window`

### Package error
Ensure `publisher` field exists in `package.json`
