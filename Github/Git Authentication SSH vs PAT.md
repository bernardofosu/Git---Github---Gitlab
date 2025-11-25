# 🔐 Git Authentication: SSH vs PAT – Canva-Ready Notes with Emojis ✨

## 🆚 SSH Keys vs GPG Keys (What’s the Difference?)

Here is a simple, clear comparison to help you understand both:

---

# 🔑 **SSH Keys (Authentication Keys)**

SSH keys are used for **logging in** or **authenticating** to GitHub.

### ✔️ Purpose

- Authenticate you when you **push/pull** code
- Replace passwords and tokens
- Secure access to GitHub servers

### ✔️ What SSH keys DO

- Allow `git push` with **no password**
- Securely identify your machine
- Used for Git operations (cloning, pulling, pushing)

### ❌ What SSH keys DO NOT do

- They do **not sign commits**
- They do **not verify authorship** of commits

---

# ✍️ **GPG Keys (Commit Signing Keys)**

GPG keys are used to **digitally sign your commits**.

### ✔️ Purpose

- Prove the commit truly came from you
- Show the green "Verified" badge on GitHub
- Prevent impersonation

### ✔️ What GPG keys DO

- Sign commits
- Sign tags
- Add security + authenticity to your Git history

### ❌ What GPG keys DO NOT do

- They do **not authenticate git push**
- They do **not replace SSH keys**

---

# 🆚 **SSH vs GPG — Quick Comparison**

| Feature                       | SSH Keys 🔑 | GPG Keys ✍️ |
| ----------------------------- | ----------- | ----------- |
| Used for pushing/pulling?     | ✔️ Yes      | ❌ No       |
| Used for commit signing?      | ❌ No       | ✔️ Yes      |
| Replaces passwords/tokens?    | ✔️ Yes      | ❌ No       |
| Shows "Verified" on GitHub?   | ❌ No       | ✔️ Yes      |
| Identifies your machine?      | ✔️ Yes      | ❌ No       |
| Identifies the commit author? | ❌ No       | ✔️ Yes      |

---

# 🎯 **Simple Explanation**

- **SSH = lets you push code** securely without entering passwords.
- **GPG = proves you truly wrote the commit**, giving you the verified badge.

Both are useful, but for different parts of the Git workflow. – Canva‑Ready Notes with Emojis ✨

A simple guide to understand why SSH and PAT behave differently when pushing to GitHub.

---

# 🆚 1. HTTPS + PAT (Personal Access Token)

When you clone or push using HTTPS, Git asks for:

- 👤 **GitHub username**
- 🔑 **GitHub PAT token** (your access token)

### ✔️ After you enter it once

If credential caching is enabled, Git **may remember it**, so you won’t always enter it again.

### ❗ But sometimes Git will ask again:

- When the token expires
- When credentials are not cached
- When using a new terminal/session
- On some servers like AWS EC2

### 🔍 Example

```
Username for 'https://github.com': bernardofosu
Password for 'https://bernardofosu@github.com': <your PAT>
```

---

# 🔑 2. SSH Key Authentication (Recommended)

SSH uses a **key pair** stored on your machine.

### ✔️ Steps:

1. Generate SSH key:

```
ssh-keygen -t ed25519
```

2. Add the public key (`id_ed25519.pub`) to GitHub.
3. Clone using SSH:

```
git clone git@github.com:username/repo.git
```

### ⭐ After setup — NO username, NO token

You push like this:

```
git push
```

And it authenticates **automatically**.

### 🎉 Why SSH is better:

- No token required
- No password prompts
- Most secure
- Ideal for servers (AWS, Azure, GCP)

---

# 🔥 PAT vs SSH – Quick Comparison

| Feature                | PAT (HTTPS)  | SSH                   |
| ---------------------- | ------------ | --------------------- |
| Needs username?        | ✔️ Yes       | ❌ No                 |
| Needs token each time? | Sometimes    | ❌ Never              |
| Best for servers?      | ❌ Not ideal | ⭐ Yes                |
| Most secure?           | Good         | ⭐ Best               |
| GitHub recommends?     | ✔️ Yes       | ⭐ Highly recommended |

---

# 🎯 Final Answer

### ✔️ **PAT:** After configuring, you _may_ not need to enter the token again.

### ✔️ **SSH:** After setup, you **NEVER** need to enter a token or password again — authentication is automatic.

---

If you want, I can create:

- 🔧 SSH setup guide
- 🔧 PAT setup guide
- 📄 Canva‑styled Git authentication cheatsheet
  Just tell me! 🎨
