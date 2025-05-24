# AI Commit Message Generator

**AI Commit Message Generator** is a powerful command-line tool that uses Claude AI to automatically generate well-structured and meaningful Git commit messages based on your staged code changes.

---

## ✨ Features

- Uses Claude AI (e.g., Claude 3.7 Sonnet) to analyze your staged `git diff`
- Generates commit messages with:
  - A concise summary line
  - Detailed bullet points of changes
- Supports flexible configuration using `.env` files or environment variables
- Offers helpful CLI flags like `--dry`, `--edit`, and `--out`
- Allows excluding specific file patterns (e.g., `*.log`, `dist/*`) from the diff using the `GITM_EXCLUDE_PATTERNS` environment variable
- Automatically copies the message to your clipboard
- Provides consistent, high-quality commit messages across your project

---

## 🧪 Example Output

```txt
Implement user authentication and improve error handling

- Add user login and registration functionality
- Implement JWT-based authentication system
- Create middleware for protected routes
- Enhance error handling in API endpoints
- Update user model with password hashing
- Add input validation for user-related operations
```

---

## 🛠 Prerequisites

Make sure the following are installed on your system:

- Git
- Bash
- `curl`
- `jq`
- `pbcopy` (on macOS) or adjust clipboard logic for your OS
- A Claude API key from [Anthropic](https://www.anthropic.com)

---

## 📦 Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/ayyazzafar/ai-commit-message-generator.git
   ```

2. Move the `gitm` script to a directory in your `PATH` (e.g., `~/bin/`):

   ```bash
   sudo mv ai-commit-message-generator/gitm /usr/local/bin/
   sudo chmod +x /usr/local/bin/gitm
   ```

3. Create a config file at `~/.config/gitm/.env` and add your API key and preferences:

   ```dotenv
   CLAUDE_API_KEY=sk-your-api-key-here
   CLAUDE_MODEL=claude-3-7-sonnet
   CLAUDE_VERSION=2023-06-01
   # Optional: Space-separated list of patterns to exclude from the diff
   # GITM_EXCLUDE_PATTERNS="*.log build/* temp/**/*.tmp"
   ```

> 🔒 **Do not store secrets in public/shared folders like `~/bin`.**

---

## 🚀 Usage

1. Stage your changes with `git add`:

   ```bash
   git add .
   ```

2. Run the generator:

   ```bash
   gitm
   ```

3. Then commit using the generated message:

   ```bash
   git commit -m "$(pbpaste)"
   ```

---

## 🧰 CLI Options

| Flag                   | Description                                                                         | Default                                        |
| ---------------------- | ----------------------------------------------------------------------------------- | ---------------------------------------------- |
| `--dry`                | Show message preview without copying or committing                                  | Not set (proceeds to copy/save)                |
| `--edit`               | Open message in your default editor before using it                                 | Not set (does not open in editor)              |
| `--out=message.txt`    | Save message to a file instead of clipboard                                         | Not set (copies to clipboard)                  |
| `--env=/path/to/.env`  | Load environment config from custom path                                            | `$HOME/.config/gitm/.env` (or `GITM_ENV_FILE`) |
| `--include-lock-files` | Include `package-lock.json` and `pnpm-lock.yaml` files in commit message generation | Not set (lock files excluded)                  |
| `--help`               | Display usage instructions                                                          | Not set (proceeds with generation)             |

---

## ⚙️ Configuration Options

You can customize the tool using:

1. A default `.env` file:

   - `~/.config/gitm/.env`

2. The `GITM_ENV_FILE` environment variable:

   ```bash
   export GITM_ENV_FILE=/secure/location/my.env
   ```

   You can also set other environment variables like `CLAUDE_MODEL`, `CLAUDE_VERSION`, or `GITM_EXCLUDE_PATTERNS` in a similar way, or within your shell's configuration file (e.g., `.zshrc`, `.bashrc`).

   Example for `GITM_EXCLUDE_PATTERNS`:

   ```bash
   export GITM_EXCLUDE_PATTERNS="*.log build/* docs/**/*.md"
   ```

3. Or directly with `--env` at runtime:

   ```bash
   gitm --env=/secure/location/my.env
   ```

---

## 🧠 How It Works

1. Captures staged changes using `
