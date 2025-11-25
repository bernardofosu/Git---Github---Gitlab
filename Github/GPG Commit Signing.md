# ✍️ GPG Commit Signing – Canva-Ready Notes with Emojis ✨

This document explains **what GPG keys are**, why they are important, and **how to sign your Git commits step-by-step**.

---

# ✍️ What Are GPG Keys?

GPG (GNU Privacy Guard) keys are cryptographic keys used to **digitally sign your Git commits and tags**.

They prove:

- ✔️ **You** made the commit
- ✔️ The commit wasn’t modified
- ✔️ The author identity is authentic
- ✔️ Shows the green **“Verified”** badge on GitHub

---

# 🎯 Why Use GPG Keys?

- 🛡️ Protects against impersonation
- 🧑‍💻 Makes your commits look professional
- 🟢 Shows a verified status on GitHub
- 🔒 Adds trust and authenticity to your project

---

# ✔️ What GPG Keys DO

- ✍️ Sign commits
- 🏷️ Sign Git tags
- 🔐 Strengthen your Git history integrity

---

# ❌ What GPG Keys DO NOT Do

- They do **not** authenticate you when pushing
- They do **not** replace SSH keys
- They do **not** log you into GitHub

➡️ **SSH = authenticate pushes**
➡️ **GPG = sign commits**

Both are separate but complementary.

---

# 🛠️ How to Generate and Use GPG Keys (Step-by-Step)

## 1️⃣ Install GPG on Your System

### Ubuntu / Debian:

```
sudo apt install gnupg
```

### macOS (Homebrew):

```
brew install gnupg
```

---

## 2️⃣ Generate a New GPG Key

Run:

```
gpg --full-generate-key
```

Choose:

- 🔑 RSA and RSA
- 🔢 4096 bits
- 📅 Expiration: 0 (never) or a chosen time
- 👤 Your name
- 📧 Your GitHub email address

---

## 3️⃣ List Your GPG Keys

```
gpg --list-secret-keys --keyid-format=long
```

You will see something like:

```
sec   rsa4096/ABCDEF1234567890 2025-11-25
```

Copy the part after the slash:
➡️ `ABCDEF1234567890`

This is your **GPG Key ID**.

---

## 4️⃣ Export Your Public Key for GitHub

```
gpg --armor --export ABCDEF1234567890
```

Copy the full block that begins with:

```
-----BEGIN PGP PUBLIC KEY BLOCK-----
```

Paste this in GitHub:

- Settings → **SSH and GPG Keys** → **New GPG Key**

---

## 5️⃣ Tell Git to Use Your GPG Key

```
git config --global user.signingkey ABCDEF1234567890
```

Enable automatic signing:

```
git config --global commit.gpgsign true
```

---

# ✍️ How to Sign a Commit

### Automatically (if enabled):

Just commit normally:

```
git commit -m "Signed commit"
```

Git will sign it using your GPG key.

### Manually (per commit):

```
git commit -S -m "Signed commit"
```

---

# 🧪 Verify a Signed Commit

```
git log --show-signature -1
```

Or on GitHub, the commit will show:

🟢 **Verified**

---

# 🎯 Summary

- **SSH → authenticate pushes**
- **GPG → sign commits**
- GPG adds security + professionalism
- GitHub shows a green verified badge when used correctly

---

If you want, I can also create:

- 🔒 SSH Setup Guide
- 🧩 Full Git Security Cheatsheet
- 🎨 A Canva-style printable page
