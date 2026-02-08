# roderick.dk

Personal website built using Hugo & Pagemod

## Setup

1. Install Node.js dependencies:

    ```sh
    npm install
    ```

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
