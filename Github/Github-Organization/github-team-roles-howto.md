# 🧩 Add Roles to a Team (Two Ways)

## 1) 🔭 Org-wide role (affects all repos)
Use this for things like **All-repository read/write/admin**, **CI/CD admin**, **Security manager**.

**Path:** `Org → Settings → Organization roles → Role assignments`  
1. Click **New role assignment**.  
2. Pick a role (e.g., **All-repository read**, **All-repository admin**, **CI/CD Admin**, **Security manager**).  
3. In **Search for users or teams**, type your team’s name *(tip: you can type `is:team` then the name)*.  
4. Click **Add new assignment** ✅

> 🔒 **Best practice:** avoid **All-repository admin** except for a tiny trusted team.

---

## 2) 📦 Repo-specific role (affects only selected repos)
Use this **90% of the time** for least-privilege access.

**Path:** `Org → Teams → Your Team → Repositories → Add repository`  
1. Choose the repo(s).  
2. Set role: **Read / Triage / Write / Maintain / Admin**.  
3. **Save**. ✅

---

## 🧠 What to choose when?

| 🎯 Goal | 🛣️ Path | 🧱 Role to use | 🔎 Notes |
|---|---|---|---|
| Give one team write access to one repo | Teams → Team → Repositories | **Write** | Most common setup. |
| Let instructors manage a course repo (merge, labels, releases) | Teams → Instructors → Repositories | **Maintain** | Powerful, but not full Admin. |
| Make a platform team manage Actions/runners org‑wide | Settings → Organization roles | **CI/CD Admin** | No need for full repo Admin. |
| Security reviewers across the org | Settings → Organization roles | **Security manager** | Review alerts & policies org‑wide. |
| Temporary read access to all repos | Settings → Organization roles | **All‑repository read** | Time‑box and remove later. |

---

## 🧹 Edit / remove later
- **Org‑wide roles:** `Settings → Organization roles → Role assignments` → **⋯** → **Remove** or **Change role**.  
- **Repo roles:** `Teams → Team → Repositories` → use the **Role** dropdown or **Remove**.

---

### ✅ Tips
- Keep *Admin* small; prefer **Maintain** for repo managers.  
- Pair with **branch protection** and **CODEOWNERS** to enforce reviews.  
- Use **secret scanning** and **role audits** regularly.
