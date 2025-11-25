# 🔑 SSH for GitHub CLI (gh) – Full Canva-Ready Notes with Emojis ✨

This document combines **all notes** from:

- Using SSH with GitHub CLI
- How GitHub CLI + SSH work together
- How SSH key selection works
- How to force SSH to use a specific key

Perfect for DevOps, AWS servers, Linux, and GitHub automation.

---

# 🟦 What Is GitHub CLI (`gh`)?

`gh` = **GitHub Command Line Interface**

It allows you to:

- 🆕 Create repositories
- 📥 Clone repos
- 🔐 Authenticate via SSH or HTTPS
- 🔁 Manage PRs & issues
- ⚙️ Trigger GitHub Actions workflows
- 🚀 Push code without touching GitHub.com

---

# 🔑 Why Use SSH With GitHub CLI?

SSH authentication means:

- ❌ No GitHub username needed
- ❌ No password
- ❌ No PAT token required every time
- ✔️ Automatic secure authentication
- ✔️ Perfect for AWS, Linux, servers, DevOps pipelines

SSH + GitHub CLI = 🔥 **Fast + Secure + Fully Automated GitOps workflow**

---

# 🛠️ Step 1 — Generate SSH Key

Recommended:

```
ssh-keygen -t ed25519 -C "your_email@example.com"
```

This creates:

- 🔐 Private key → `~/.ssh/id_ed25519`
- 🔓 Public key → `~/.ssh/id_ed25519.pub`

If you used a custom name:

```
ssh-keygen -t ed25519 -f ~/.ssh/mycustomgithubkey
```

Your keys become:

- Private: `mycustomgithubkey`
- Public: `mycustomgithubkey.pub`

---

# 🟠 Step 2 — Add SSH Key to the SSH Agent

```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

If custom key:

```
ssh-add ~/.ssh/mycustomgithubkey
```

---

# 🔐 Step 3 — Upload SSH Key to GitHub Using GitHub CLI

```
gh ssh-key add ~/.ssh/id_ed25519.pub --title "AWS VM Key"
```

Or custom name:

```
gh ssh-key add ~/.ssh/mycustomgithubkey.pub --title "Custom Key"
```

This saves the public key to GitHub.

---

# 🟦 Step 4 — Tell GitHub CLI To Use SSH

```
gh config set -h github.com git_protocol ssh
```

From now on:

- `gh repo clone` uses SSH URL
- `gh repo create` configures SSH remote
- `git push` uses SSH automatically

---

# 🚀 Step 5 — Create a Repo Using SSH + GH CLI

```
gh repo create myproject --public
```

GitHub CLI automatically sets the SSH remote:

```
git@github.com:USERNAME/myproject.git
```

---

# 📥 Step 6 — Clone Repos Over SSH

```
gh repo clone username/repo
```

Your clone URL looks like:

```
git@github.com:username/repo.git
```

---

# 📤 Step 7 — Push Code With SSH (No Password!)

```
git push
```

SSH automatically authenticates.
No PAT.
No username.
No prompt.

---

# ⭐ How Does SSH Know Which Private Key To Use?

SSH checks keys in the following order:

### 1️⃣ SSH Agent (Most Important)

SSH uses any key you added with:

```
ssh-add <key>
```

If the agent contains a key that matches GitHub’s public key → SSH uses it.

### 2️⃣ Default Key Names

If no keys are in the agent, SSH tries:

```
~/.ssh/id_ed25519
~/.ssh/id_rsa
~/.ssh/id_ecdsa
```

### 3️⃣ Any Key in ~/.ssh

SSH will try other private keys in the `~/.ssh` folder.
If GitHub matches the public key → it works.

### ✔️ GitHub CLI does NOT pick the SSH key.

### ✔️ SSH automatically selects the correct one.

---

# 🔧 How To Force SSH To Use a Specific Key

Create or edit:

```
nano ~/.ssh/config
```

Add:

```
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/mycustomgithubkey
    IdentitiesOnly yes
```

This ensures:

- SSH only uses **this specific key**
- No confusion
- Perfect for multiple GitHub accounts

---

# 🟠 Using a Custom-Named SSH Key

If you generated a key with a custom name:

```
ssh-keygen -t ed25519 -f ~/.ssh/custom_github_key -C "your_email@example.com"
```

You will get:

- 🔐 Private key → `~/.ssh/custom_github_key`
- 🔓 Public key → `~/.ssh/custom_github_key.pub`

### ✔ Add the custom key to SSH agent

```
ssh-add ~/.ssh/custom_github_key
```

### ✔ Upload custom public key to GitHub

```
gh ssh-key add ~/.ssh/custom_github_key.pub --title "Custom SSH Key"
```

### ✔ Force GitHub SSH to use the custom key (optional)

Update `~/.ssh/config`:

```
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/custom_github_key
    IdentitiesOnly yes
```

This guarantees GitHub will always use the specific custom SSH key for authentication.
Create or edit:

```
nano ~/.ssh/config
```

Add:

```
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/mycustomgithubkey
    IdentitiesOnly yes
```

This ensures:

- SSH only uses **this specific key**
- No confusion
- Perfect for multiple GitHub accounts

---

# 🧩 SSH + GH CLI Cheat Sheet

| Action               | Command                                        |
| -------------------- | ---------------------------------------------- |
| Generate key         | `ssh-keygen -t ed25519`                        |
| Add key to agent     | `ssh-add ~/.ssh/id_ed25519`                    |
| Add key to GitHub    | `gh ssh-key add ~/.ssh/id_ed25519.pub`         |
| Switch GH CLI to SSH | `gh config set -h github.com git_protocol ssh` |
| Create repo          | `gh repo create <name>`                        |
| Clone repo           | `gh repo clone user/repo`                      |
| Push code            | `git push`                                     |
| Test SSH             | `ssh -T git@github.com`                        |

---

# 🎯 Final Summary

- SSH + GH CLI gives **password-free, secure GitHub automation**
- GH CLI uses SSH to:

  - clone
  - create repos
  - push code
  - authenticate seamlessly

- SSH key selection is done by the **SSH client**, not `gh`
- Use `~/.ssh/config` to control which SSH key is used

---

If you'd like, I can merge this with your SSH or GitHub CLI canvas documents or export as a PDF. 🎨
