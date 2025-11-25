# 🔐 How to Set Azure DevOps Credentials to Push Code (Canva Notes with Emojis)

Pushing code to **Azure DevOps Repos** from your terminal requires authentication. Azure supports two secure methods:

---

# 🟦 1. Authenticate Using HTTPS + PAT (Personal Access Token)

This is the **easiest** and most common method.

## ⭐ Step 1 — Create a PAT Token

1. Go to **User Settings → Personal Access Tokens**
2. Click **New Token**
3. Set scopes:

   - ✔ **Code: Read & Write**

4. Click **Create**
5. Copy the token (you won’t see it again!)

## ⭐ Step 2 — Push Using HTTPS

When running:

```
git push -u origin main
```

Azure will ask:

- **Username:** your Azure DevOps username or email
- **Password:** your **PAT token** (NOT your real password)

## ⭐ Step 3 — Save Credentials (Optional)

To avoid entering PAT every time:

```
git config --global credential.helper store
```

Credentials will be saved in `~/.git-credentials`.

---

# 🟪 2. Authenticate Using SSH Keys (Best for Servers like AWS VM)

SSH is more secure for automation.

## ⭐ Step 1 — Generate SSH Key

```
ssh-keygen -t ed25519 -C "you@example.com"
```

Creates:

- 🔐 Private key → `~/.ssh/id_ed25519`
- 🔓 Public key → `~/.ssh/id_ed25519.pub`

## ⭐ Step 2 — Add SSH Key to Azure DevOps

Go to: **User Settings → SSH Public Keys** → Add Key → paste:

```
cat ~/.ssh/id_ed25519.pub
```

## ⭐ Step 3 — Use SSH Clone URL

Azure gives you an SSH URL like:

```
git@ssh.dev.azure.com:v3/ORG/PROJECT/REPO
```

Add it:

```
git remote add origin git@ssh.dev.azure.com:v3/ORG/PROJECT/_git/REPO
```

Push:

```
git push -u origin main
```

---

# 🟨 Summary Table: HTTPS vs SSH

| Method         | Best For             | Pros                 | Cons                       |
| -------------- | -------------------- | -------------------- | -------------------------- |
| 🔵 HTTPS + PAT | Desktop use          | Easy                 | Requires PAT unless stored |
| 🟣 SSH Keys    | Servers (AWS, Linux) | No passwords; secure | Requires setup             |

---

# 🎯 Final Notes

- ✔ You **must** add a remote first:
  `git remote add origin <URL>`
- ✔ Azure DevOps **never auto-creates remotes** (unlike VS Code for GitHub)
- ✔ PAT or SSH is required before you can push

If you want, I can also add diagrams or convert these notes into a polished Canva-ready PDF! 🎨✨
