
# 🧩 GitHub Teams: **Repo‑Scoped Permissions** (Not Org‑Wide Roles)

> **Goal:** Keep the org locked down. **Do not** give teams org‑wide roles. Instead, add repositories to each team and set a **per‑repo role**. When you add members to a team, they **inherit only those repo permissions**. 🔐

---

## ✅ Quick Principles

- 🧱 **Org base permission:** `Read` (members not on a team are read‑only).
- 🚫 **Org‑wide role assignments for teams:** **Avoid** (e.g., *All‑repository write/admin*).  
- 🧩 **Team access = list of repos + a role per repo** (`Read` / `Triage` / `Write` / `Maintain` / `Admin`).
- 🧑‍🤝‍🧑 Add people to teams → they inherit the team’s **repo‑scoped** permissions only.

---

## 🛠️ How To (UI)

1) **Create or open a team** → `Org Home → Teams → <team>`  
2) **Repositories** tab → **Add repository** → pick a repo → **Add repository to team**  
3) Click the **Role** pill and choose:  
   - `Read` 📖 — view/clone, comment  
   - `Triage` 🧹 — manage issues/PRs (no push)  
   - `Write` ✍️ — push code + issues/PRs  
   - `Maintain` 🛠️ — manage settings/release/branches (no full Admin)  
   - `Admin` 👑 — full repo admin  
4) **Members** tab → **Add people** → (optionally mark some as **Maintainers** to manage the team).

> **Where *not* to click:** `Settings → Organization roles → Role assignments`. Those grant **org‑wide** access and bypass your least‑privilege model. 🙅‍♂️

---

## 📦 Recommended Layout (example for NakodTech)

| Team | Purpose | Example Repos | Role |
|---|---|---|---|
| 👑 `admins` | Own settings/secrets | `infra`, `billing`, `*` (select few) | Admin |
| 🧑‍🏫 `instructors` | Teach, review, merge | `courses/*`, `labs/*` | Maintain |
| 🧰 `maintainers` | Day‑to‑day caretaking | `website`, `templates` | Maintain |
| ✍️ `students` | Do lab work only | `labs/*` | Write |
| 🛡️ `security` | Triage vulns | all product repos | Triage |
| 🔧 `platform` | CI/CD & runners | `infra`, `pipelines` | Maintain |
| 🤖 `bots` | Automation | scoped repos | Write |

> Pair with branch protection (required reviews, status checks, restrict who can push to protected branches).

---

## 🔎 Verify Least‑Privilege

- Create a **test user** with **no team** → can only **Read** repos.  
- Add same user to `students` → can push to **lab** repos, but nowhere else.  
- Mention `@org/instructors` on a PR → team gets notified (if **Visible** team & notifications **Enabled**).

---

## 🧯 Common Pitfalls

- **Org‑wide roles** (e.g., *All‑repository write*) accidentally make every repo writable. Use **per‑repo** roles instead.  
- **Private forks** allowed → can leak code. Keep *Allow forking of private repos* **Off**.  
- **No team on write:** People push from direct invites. Prefer **Teams** for any write/admin access for auditability.

---

## 🧪 CLI / API (optional)

**gh** (GitHub CLI):

```bash
# grant a team 'maintain' on a repo
gh api \
  -X PUT \
  -H "Accept: application/vnd.github+json" \
  "/orgs/NakodTech-DevSecops-Academy/teams/instructors/repos/NakodTech-DevSecops-Academy/DevSecops" \
  -f permission=maintain
```

**REST (curl):**

```bash
curl -s -H "Authorization: Bearer $GH_TOKEN" \
  -H "Accept: application/vnd.github+json" \
  -X PUT \
  https://api.github.com/orgs/NakodTech-DevSecops-Academy/teams/students/repos/NakodTech-DevSecops-Academy/labs-demo \
  -d '{"permission":"push"}'   # push = Write
```

---

## ✅ Outcome

- Members **not on teams** → **Read‑only** everywhere.  
- Teams → **exact repo roles** only.  
- Org stays **locked down** while instructors/maintainers get the access they need. 💪
