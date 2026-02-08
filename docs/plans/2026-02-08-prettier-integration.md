# Prettier Integration Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add Prettier for automatic code formatting via PostToolUse hook and pre-commit git hook.

**Architecture:** Use Prettier with Husky for git hook management and lint-staged to format only staged files. PostToolUse hook in Claude Code settings runs Prettier after file edits.

**Tech Stack:** Prettier, Husky, lint-staged, npm

---

## Task 1: Create package.json

**Files:**

- Create: `package.json`

**Step 1: Write package.json**

Create the file with Prettier, Husky, and lint-staged dependencies:

```json
{
    "name": "roderick.dk",
    "version": "1.0.0",
    "private": true,
    "scripts": {
        "prepare": "husky"
    },
    "devDependencies": {
        "husky": "^9.1.7",
        "lint-staged": "^15.2.11",
        "prettier": "^3.4.2"
    },
    "lint-staged": {
        "*.{md,yaml,yml,json,html,js}": "prettier --write"
    }
}
```

**Step 2: Verify file created**

Run: `cat package.json`
Expected: File contents match above

**Step 3: Commit**

```bash
git add package.json
git commit -m "chore: add package.json with Prettier dependencies"
```

---

## Task 2: Create Prettier configuration

**Files:**

- Create: `.prettierrc`

**Step 1: Write .prettierrc**

Create configuration with single override:

```json
{
    "trailingComma": "none"
}
```

**Step 2: Verify file created**

Run: `cat .prettierrc`
Expected: File contents match above

**Step 3: Commit**

```bash
git add .prettierrc
git commit -m "chore: configure Prettier with no trailing commas"
```

---

## Task 3: Create Prettier ignore file

**Files:**

- Create: `.prettierignore`

**Step 1: Write .prettierignore**

Create ignore patterns for build outputs and dependencies:

```
public/
resources/
node_modules/
.hugo_build.lock
package-lock.json
```

**Step 2: Verify file created**

Run: `cat .prettierignore`
Expected: File contents match above

**Step 3: Commit**

```bash
git add .prettierignore
git commit -m "chore: configure Prettier ignore patterns"
```

---

## Task 4: Update Claude Code settings

**Files:**

- Modify: `.claude/settings.json`

**Step 1: Read current settings**

Run: `cat .claude/settings.json 2>/dev/null || echo "{}"`
Expected: Empty or existing JSON

**Step 2: Update settings.json**

Add PostToolUse hooks (for Edit and Write only) and permissions:

```json
{
    "hooks": {
        "PostToolUse(Edit)": "npx prettier --write {{file_paths}}",
        "PostToolUse(Write)": "npx prettier --write {{file_paths}}"
    },
    "permissions": {
        "allow": [
            "Bash(npm install:*)",
            "Bash(npx prettier:*)",
            "Bash(npx husky:*)"
        ]
    }
}
```

If file exists with content, merge the hooks and permissions sections appropriately.

**Step 3: Verify settings updated**

Run: `cat .claude/settings.json`
Expected: Contains hooks section with PostToolUse(Edit) and PostToolUse(Write), and permissions section with all three bash permissions

**Step 4: Commit**

```bash
git add .claude/settings.json
git commit -m "chore: add Prettier PostToolUse hook and permissions"
```

---

## Task 5: Update README

**Files:**

- Modify: `README.md`

**Step 1: Read current README**

Run: `cat README.md`
Expected: See current structure

**Step 2: Replace content**

Update README with setup instructions:

````markdown
# roderick.dk

Personal website built using Hugo & Pagemod

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

````

**Step 3: Verify README updated**

Run: `cat README.md`
Expected: Contains Setup section with npm install and Code Formatting section

**Step 4: Commit**

```bash
git add README.md
git commit -m "docs: update README with setup and formatting instructions"
````

---

## Task 6: Install dependencies

**Files:**

- Creates: `package-lock.json`, `node_modules/`

**Step 1: Run npm install**

Run: `npm install`
Expected: Installs prettier, husky, lint-staged
Output shows packages installed

**Step 2: Verify installation**

Run: `npx prettier --version`
Expected: Version number displayed (e.g., 3.4.2)

Run: `npx husky --version`
Expected: Version number displayed (e.g., 9.1.7)

**Step 3: Commit lockfile**

```bash
git add package-lock.json
git commit -m "chore: add package-lock.json"
```

Note: `node_modules/` should not be committed (add to .gitignore if needed)

---

## Task 7: Initialize Husky

**Files:**

- Creates: `.husky/pre-commit`

**Step 1: Run husky init**

Run: `npx husky init`
Expected: Creates `.husky/` directory with pre-commit hook

**Step 2: Verify pre-commit hook**

Run: `cat .husky/pre-commit`
Expected: File exists with npx lint-staged command

**Step 3: Make hook executable**

Run: `chmod +x .husky/pre-commit`
Expected: No output

**Step 4: Verify hook is executable**

Run: `ls -l .husky/pre-commit`
Expected: Shows execute permissions (-rwxr-xr-x)

**Step 5: Commit Husky setup**

```bash
git add .husky/
git commit -m "chore: initialize Husky for git hooks"
```

---

## Task 8: Format existing files

**Files:**

- Modifies: All `.md`, `.yaml`, `.yml`, `.json` files in project

**Step 1: Run Prettier on all files**

Run: `npx prettier --write .`
Expected: Output shows files being formatted
Example: "hugo.yaml 50ms", "README.md 25ms"

**Step 2: Check what changed**

Run: `git status`
Expected: Shows modified files (likely yaml, json, markdown files)

Run: `git diff --stat`
Expected: Shows summary of changes

**Step 3: Review changes**

Run: `git diff` (or check a few key files)
Expected: Only formatting changes (whitespace, line endings, etc)

**Step 4: Commit formatted files**

```bash
git add -A
git commit -m "style: format all files with Prettier"
```

---

## Task 9: Verify PostToolUse hook

**Files:**

- Test: Create temporary file to verify hook

**Step 1: Create test markdown file**

Run: `echo "# Test\nThis    has   weird    spacing" > test-formatting.md`
Expected: File created

**Step 2: Check file formatting**

Run: `cat test-formatting.md`
Expected: Shows unformatted content with weird spacing

**Step 3: Manually format with Prettier**

Run: `npx prettier --write test-formatting.md`
Expected: File formatted

**Step 4: Check formatted result**

Run: `cat test-formatting.md`
Expected: Shows properly formatted content (single spaces)

**Step 5: Clean up test file**

Run: `rm test-formatting.md`
Expected: File removed

Note: PostToolUse hook only triggers when Claude Code edits files, not manual commands. This verifies Prettier works correctly when the hook calls it.

---

## Task 10: Verify pre-commit hook

**Files:**

- Test: Stage and commit a file to trigger hook

**Step 1: Create test file with bad formatting**

Run: `echo "test:    value" > test-commit.yaml`
Expected: File created with extra spaces

**Step 2: Stage the file**

Run: `git add test-commit.yaml`
Expected: File staged

**Step 3: Attempt commit**

Run: `git commit -m "test: verify pre-commit hook"`
Expected: Hook runs, formats file, commits successfully
Output shows lint-staged running Prettier

**Step 4: Verify file was formatted**

Run: `cat test-commit.yaml`
Expected: `test: value` (single space)

**Step 5: Check commit succeeded**

Run: `git log --oneline -1`
Expected: Shows "test: verify pre-commit hook" commit

**Step 6: Clean up test commit**

Run: `git reset --soft HEAD~1`
Expected: Uncommits last commit, keeps changes staged

Run: `git reset HEAD test-commit.yaml`
Expected: Unstages file

Run: `rm test-commit.yaml`
Expected: Removes test file

---

## Task 11: Final verification

**Files:**

- None (verification only)

**Step 1: Check all config files exist**

Run: `ls -1 package.json .prettierrc .prettierignore .husky/pre-commit .claude/settings.json`
Expected: All files listed

**Step 2: Verify Prettier works**

Run: `npx prettier --check .`
Expected: "All matched files use Prettier code style!"

**Step 3: Check git status is clean**

Run: `git status`
Expected: "nothing to commit, working tree clean"

**Step 4: Review all commits**

Run: `git log --oneline`
Expected: Shows all commits from this implementation in logical order

---

## Success Criteria

- [ ] package.json created with correct dependencies
- [ ] .prettierrc configured with trailingComma: "none"
- [ ] .prettierignore excludes build outputs
- [ ] .claude/settings.json has PostToolUse hook and permissions
- [ ] README.md updated with setup instructions
- [ ] Dependencies installed (node_modules/, package-lock.json)
- [ ] Husky initialized with pre-commit hook
- [ ] All existing files formatted with Prettier
- [ ] Prettier check passes on all files
- [ ] Git status clean after all changes committed

## Next Steps

After implementation:

1. Use @superpowers:finishing-a-development-branch to integrate the work
2. Consider creating PR for review if working with team
3. Test in real usage by editing files with Claude Code
