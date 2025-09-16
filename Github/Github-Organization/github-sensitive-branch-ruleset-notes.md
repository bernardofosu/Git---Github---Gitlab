
# 🔒 GitHub Ruleset for **Sensitive Branches** (e.g., `main`, `release/*`)

**Goal:** stop direct pushes & risky actions on your most important branches. All changes flow via Pull Requests with reviews ✅.

---

## 🚦 Outcome
- ❌ No direct pushes to `main`  
- 🔀 Changes only via **PR** with **review + passing checks**  
- 🧱 No force-push or deletion  
- 🪪 Only a small **admins** team can bypass (for emergencies)

---

## ✅ Prereqs
- You’re an **Org Owner** or **Repo Admin**.  
- Teams created (e.g., `admins`, `instructors`).  
- 🔐 Recommended org basics: 2FA required, base permission = **Read**.

> 💡 If you see a banner like *“rulesets won’t be enforced on this private repo until you upgrade”*, use **classic Branch protection** instead (steps below) or upgrade to **GitHub Team/Enterprise**.

---

## 🧩 Steps — **Ruleset (modern)**
1. Repo → **Settings** → **Rules** → **Rulesets** → **New ruleset**.  
2. **Ruleset name:** `protect-main-pr-only`  
3. **Enforcement:** **Enabled** (or *Evaluate* first to dry‑run).  
4. **Bypass list** ➕: add `@org/admins` (and any release bot/App if needed).  
5. **Target branches** 🎯: add `main` (and/or patterns like `release/*`, `hotfix/*`).  
6. **Select rules** (see explanations below):  
   - ☑️ **Restrict updates**  
   - ☑️ **Restrict deletions**  
   - ☑️ **Require a pull request before merging**  
     - Approvals required: **1–2**  
     - ☑️ **Require approval of the most recent reviewable push**  
     - ☑️ **Require conversation resolution before merging**
   - ☑️ **Block force pushes**  
   - 🔬 **Require status checks to pass** (pick CI checks once they appear)  
   - ✍️ **Require signed commits** (optional but recommended)  
   - 📈 **Require linear history** *(optional; use if you only want fast‑forwards)*  
   - 🔧 **Allowed merge methods**: allow **Squash** (common) and disable others if desired  
   - 🕵️ **Require code scanning results** *(optional—needs Code Scanning setup)*  
7. **Save** → **Test** (try a direct push; it should be blocked ✅).

---

## 🔁 Fallback — **Classic Branch Protection**
If rulesets aren’t available for your plan:  
Repo → **Settings** → **Branches** → **Add rule** → pattern `main` → enable the same items:  
- Require PRs, **1–2 approvals**, **most recent approval**, **conversation resolution**  
- Require status checks, block force pushes, restrict who can push (set to **no one**), restrict deletions  
- Signed commits / linear history (optional)

---

## 🧠 Major Rules — What & Why

| ⚙️ Rule | 📝 What it does | 🤔 Why it matters | ⭐ Recommendation |
|---|---|---|---|
| 🔐 **Restrict updates** | Blocks direct pushes to the branch. | Forces changes through PRs → visibility & reviews. | **On** |
| 🛑 **Restrict deletions** | Prevents deleting the branch. | Protects default/release branches from mistakes. | **On** |
| 🔀 **Require PR before merging** | All changes must come via PR. | Enables reviews, checks, audit trail. | **On** |
| ✅ **Approvals required** | Minimum reviewer approvals. | Catches issues; pair with CODEOWNERS. | **1–2** |
| 🔁 **Most recent approval** | New commits re‑require approval. | Stops “post‑approval sneaks.” | **On** |
| 💬 **Conversation resolution** | All PR threads must be resolved. | Ensures feedback is addressed. | **On** |
| 🧪 **Status checks** | CI tests/security checks must pass. | Prevents breaking builds. | **On** (select checks) |
| 🧱 **Block force pushes** | Disables history rewrites. | Keeps audit history intact. | **On** |
| ✍️ **Signed commits** | Require GPG/SSH signatures. | Authenticates commit authors. | **On** if possible |
| 📈 **Linear history** | Disallows merge commits. | Cleaner history; easier bisects. | Optional |
| 🔧 **Allowed merge methods** | Limit to Squash/Rebase/Merge. | Enforce history style. | Squash only (common) |
| 🪪 **Bypass list** | Teams/roles that can bypass. | Emergency/unblock path. | Keep **tiny** (`admins`) |
| 🎯 **Target branches** | Which branches are protected. | Scope to `main`, `release/*`. | **Tight scope** |

---

## 🧱 Minimal → Strict Presets

**Standard (safe for most teams):**  
- Restrict updates/deletions, PR required, 1 approval, status checks, block force push.

**Strict (prod-grade):**  
- All Standard + 2 approvals, signed commits, linear history, squash only.

**Ultra (regulated):**  
- Strict + code scanning required, CODEOWNERS review required, limited bypass to 1–2 owners.

---

## 🧪 Verify
- 👤 Non-admin tries to push to `main` → 🚫 blocked.  
- 🔀 Open PR → 🧪 checks run → ✅ approvals collected → **Merge** allowed.  
- 👑 `@org/admins` can bypass in emergencies (use rarely).

---

## 📎 Helpful files
- `.github/CODEOWNERS` → routes PRs to reviewers (e.g., `* @org/instructors`).  
- `.github/SECURITY.md` → how to report vulnerabilities.  
- `.github/pull_request_template.md` → checklist for reviewers.

---

## 🧯 Tips
- Start with **Evaluate** mode to preview impacts.  
- Add a **release bot**/**CI app** to the bypass list only if it truly needs it.  
- Document your policy in `CONTRIBUTING.md` and pin it in the repo.

---

Happy hardening! 🛡️
