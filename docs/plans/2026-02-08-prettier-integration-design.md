# Prettier Integration Design

## Overview

Add Prettier to format Markdown, YAML, JSON, HTML, and JavaScript files automatically through two hooks:

1. PostToolUse hook: Formats files after Claude Code edits them
2. Pre-commit hook: Formats staged files before commits

## Configuration

### Prettier Rules

Use Prettier defaults except:

- `trailingComma: "none"` - No trailing commas

### Files to Format

- Markdown: `*.md` (blog posts, README, docs)
- YAML: `*.yaml`, `*.yml` (hugo.yaml config)
- JSON: `*.json` (settings, package files)
- HTML: `*.html` (Hugo templates if added)
- JavaScript: `*.js` (custom scripts if added)

### Files to Ignore

Create `.prettierignore`:

- `public/` - Hugo build output
- `resources/` - Hugo asset cache
- `node_modules/` - npm packages
- `.hugo_build.lock` - Hugo build artifact
- `package-lock.json` - Generated lockfile

## Implementation

### Dependencies

Add to `package.json` devDependencies:

- `prettier` - Core formatting tool
- `husky` - Manages git hooks
- `lint-staged` - Runs Prettier only on staged files

### PostToolUse Hook

Add to `.claude/settings.json`:

```json
"hooks": {
  "PostToolUse(Edit)": "npx prettier --write {{file_paths}}",
  "PostToolUse(Write)": "npx prettier --write {{file_paths}}"
}
```

Runs after Edit and Write tool calls only. Formats the modified files automatically.

### Pre-commit Hook

Configure lint-staged in `package.json`:

```json
"lint-staged": {
  "*.{md,yaml,yml,json,html,js}": "prettier --write"
}
```

Setup via Husky:

1. Run `npx husky init` to create `.husky/` directory
2. Husky creates `.husky/pre-commit` that runs lint-staged
3. lint-staged formats staged files and stages the changes
4. Commit proceeds automatically

### Permissions

Add to `.claude/settings.json`:

```json
"permissions": {
  "allow": [
    "Bash(npm install:*)",
    "Bash(npx prettier:*)",
    "Bash(npx husky:*)"
  ]
}
```

Project-wide permissions let anyone run setup commands.

## Setup Steps

1. Create `package.json` with dependencies
2. Create `.prettierrc` with trailing comma config
3. Create `.prettierignore` with exclusions
4. Update `.claude/settings.json` with hook and permissions
5. Update `README.md` with setup instructions
6. Run `npm install` to install dependencies
7. Run `npx husky init` to setup git hooks
8. Run `npx prettier --write .` to format existing files
9. Commit all changes

## README Updates

Add setup section:

````markdown
## Setup

1. Install Node.js dependencies:
    ```sh
    npm install
    ```
````

2. Install Hugo modules:

    ```sh
    hugo mod tidy
    ```

3. Run development server:
    ```sh
    hugo server
    ```

## Code Formatting

This project uses Prettier for automatic code formatting:

- Files auto-format after edits in Claude Code
- Pre-commit hook formats staged files before commits
- Manual formatting: `npx prettier --write .`

```

## Edge Cases

### Hook Failures

- PostToolUse: Shows error but doesn't block Claude Code
- Pre-commit: Blocks commit if formatting fails
- Bypass: Use `git commit --no-verify` (not recommended)

### File Types

- Binary files: Ignored automatically by Prettier
- Generated files: Listed in `.prettierignore`
- Hugo templates: Will format if added to the project

### Verification

Test the setup:
1. Edit a markdown file in Claude Code, verify formatting
2. Stage and commit a file, verify pre-commit runs
3. Run `npx prettier --check .` to verify all files formatted

## Files Changed

**New:**
- `package.json` - Dependencies and lint-staged config
- `.prettierrc` - Single trailing comma setting
- `.prettierignore` - Exclusion patterns
- `.husky/pre-commit` - Git hook (generated)
- `package-lock.json` - Dependency lock (generated)

**Modified:**
- `.claude/settings.json` - Hook and permissions
- `README.md` - Setup instructions

**Unchanged:**
- `.claude/settings.local.json` - Keep existing permissions
- All content and Hugo configuration files
```
