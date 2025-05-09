
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
````

---

## 🛠 Prerequisites

Make sure the following are installed on your system:

* Git
* Bash
* `curl`
* `jq`
* `pbcopy` (on macOS) or adjust clipboard logic for your OS
* A Claude API key from [Anthropic](https://www.anthropic.com)

---

## 📦 Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/ayyazzafar/ai-commit-message-generator.git
   ```

2. Move the `gitm` script to a directory in your `PATH` (e.g., `~/bin/`):

   ```bash
   mv ai-commit-message-generator/gitm ~/bin/
   chmod +x ~/bin/gitm
   ```

3. Create a config file at `~/.config/gitm/.env` and add your API key and preferences:

   ```dotenv
   CLAUDE_API_KEY=sk-your-api-key-here
   CLAUDE_MODEL=claude-3-7-sonnet
   CLAUDE_VERSION=2023-06-01
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

| Flag                  | Description                                         |
| --------------------- | --------------------------------------------------- |
| `--dry`               | Show message preview without copying or committing  |
| `--edit`              | Open message in your default editor before using it |
| `--out=message.txt`   | Save message to a file instead of clipboard         |
| `--env=/path/to/.env` | Load environment config from custom path            |
| `--help`              | Display usage instructions                          |

---

## ⚙️ Configuration Options

You can customize the tool using:

1. A default `.env` file:

   * `~/.config/gitm/.env`

2. The `GITM_ENV_FILE` environment variable:

   ```bash
   export GITM_ENV_FILE=/secure/location/my.env
   ```

3. Or directly with `--env` at runtime:

   ```bash
   gitm --env=/secure/location/my.env
   ```

---

## 🧠 How It Works

1. Captures staged changes using `git diff --cached`
2. Sends the diff to Claude AI with a custom prompt
3. Receives a cleanly formatted commit message
4. Copies it to clipboard, saves to file, or previews as needed

---

## 🛠 Customization

You can modify the prompt structure inside the script by editing the `content` field of the payload. This allows you to:

* Change the formatting
* Add language/style rules
* Include commit message policies

---

## 🤝 Contributing

Pull requests are welcome. Feel free to fork the repo and suggest:

* Additional flags or integrations
* OS compatibility improvements (e.g., Linux clipboard support)
* Prompt tuning

---

## 📄 License

MIT License — see the [LICENSE](LICENSE) file for full details.

---

## ⚠️ Disclaimer

This tool depends on the Anthropic Claude API. You are responsible for managing your API usage, billing, and compliance with [Anthropic's Terms of Service](https://www.anthropic.com/legal/terms-of-service). Messages generated may need human review before committing.


