# 🟦 GitHub CLI (gh) – Canva-Ready Notes with Emojis ✨

These notes explain what **GitHub CLI** is, how to install it, how to log in, how to create repositories directly from terminal, and essential commands.

---

# 🔵 What is `gh`?

`gh` = **GitHub CLI (Command Line Interface)**

It allows you to use GitHub **from the terminal**, including:

- 🆕 Creating repositories automatically
- 🧑‍💻 Authenticating with GitHub
- 📥 Cloning repositories
- 🔁 Managing pull requests & issues
- ⚙️ Running workflows
- 🚀 Pushing code without visiting GitHub.com

---

# 🛠️ Install GitHub CLI on Ubuntu

Run:

```
sudo apt install gh
```

Verify installation:

```
gh --version
```

---

# 🔐 Log In to GitHub CLI

Run:

```
gh auth login
```

Choose:

- 🌍 **GitHub.com**
- 🔐 **HTTPS**
- ✔️ Authenticate Git
- 🪪 Paste your **GitHub Personal Access Token (PAT)**

Required PAT Scopes:

- `repo`
- `read:org`
- `workflow`

Successful login message:

```
✓ Logged in as <your-username>
```

---

# 🚀 Create a GitHub Repo from CLI

This is the main benefit of GitHub CLI.

Create a **public** repo:

```
gh repo create <repo-name> --public
```

Create a **private** repo:

```
gh repo create <repo-name> --private
```

Example:

```
gh repo create try-2 --public
```

Output:

```
✓ Created repository bernardofosu/try-2 on GitHub
```

🔥 **Note:** This works even on AWS VM CLI because `gh` uses the GitHub API to auto-create the repo.

---

# 🟦 Why GitHub CLI Works but Normal CLI Does NOT

### ✔️ GitHub CLI (`gh`) uses the GitHub API → auto-creates repository

### ❌ Normal Git CLI **cannot** create remote repos

This is why you must create a repo manually when using:

- AWS VM terminal
- Linux terminal
- Mac terminal
- Windows CMD/PowerShell

But with GitHub CLI:
➡️ You can push directly without creating the repo on the website.

---

# 📦 Clone a Repo

```
gh repo clone username/repo
```

---

# 📋 Basic `gh` Commands Cheat Sheet

| Purpose              | Command                       |
| -------------------- | ----------------------------- |
| Login                | `gh auth login`               |
| Logout               | `gh auth logout`              |
| Check auth           | `gh auth status`              |
| Create repo          | `gh repo create <name>`       |
| Clone repo           | `gh repo clone <user>/<repo>` |
| Open repo in browser | `gh repo view --web`          |
| List repos           | `gh repo list`                |
| Create issue         | `gh issue create`             |
| List PRs             | `gh pr list`                  |
| Checkout PR          | `gh pr checkout <number>`     |

---

# 🎯 Final Summary

- ✔️ `gh` = GitHub power from the terminal
- ✔️ Allows creating GitHub repos directly from CLI
- ✔️ Perfect for AWS VM, Ubuntu, servers, DevOps
- ✔️ No need to open GitHub.com
- ❌ Normal `git` cannot create repos
- 🔐 Requires PAT login

---

If you'd like, I can create:

- 📄 A full GitHub CLI cheat sheet
- 🎨 Printable Canva design
- 🧰 DevOps terminal command guide
