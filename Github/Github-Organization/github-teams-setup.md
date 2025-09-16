# 🧩 Create Teams in a GitHub Organization

## ✅ UI Steps (fastest)

1. **Org Home → Teams → New team**  
   _(From your screenshot, you’re already here—perfect!)_
2. **Team name:** e.g., Admins, Instructors, Students, Security  
   - Keep names short, lowercase slug‑friendly (used for `@org/team` mentions).
3. **Description:** What this team does (helps later with audits).
4. **Parent team (optional):** Use if you want **nested teams** (members inherit access from parent).
5. **Team visibility:**  
   - **Visible** (recommended) → everyone in the org can see & mention the team.  
   - **Secret** → only team members & owners can see it (good for security/vendor teams).
6. **Team notifications:** **Enabled** (so `@org/team` pings the right people).
7. **Create team** → then:
   - **Members** tab → **Add people**  
     - **Maintainers** (can manage team & repos)  
     - **Members** (normal contributors)
   - **Repositories** tab → **Add repository** → choose role: **Read / Triage / Write / Maintain / Admin**  
     _(Use **Triage** for issue‑only helpers, **Maintain** for repo managers without full Admin.)_

---

## 🧱 Recommended Team Layout (for NakodTech DevSecOps Academy)

| 👥 Team | 🎯 Purpose | 🔧 Default Repo Role | 🔑 Key Privileges | 📝 Notes |
|---|---|---|---|---|
| 👑 **admins** | Org/repo admins | Admin (specific repos) | Manage settings, secrets, protection rules | Keep small; org owners are separate from teams |
| 🧑‍🏫 **instructors** | Teach, review, merge PRs | Maintain | Merge, label, manage branches (no destructive admin) | Pair with branch protections |
| 🧰 **maintainers** | Repo caretakers | Maintain | Releases, labels, branch rules | For non‑teaching maintainers |
| ✍️ **students** | Learners/labs | Write (only lab repos) | Push to lab repos, PRs | Read everywhere else |
| 🛡️ **security** | Vulnerability triage | Triage or Maintain | Review security alerts, labels, workflows | Make **Secret** if needed |
| 🏗️ **platform** | Infra/CI folks | Maintain | Pipelines, runners, actions | Limited number of repos |
| 🤖 **bots** | Automation accounts | Write (scoped) | PRs, releases | Use fine‑grained PATs / GitHub Apps |

> 💡 **Tip:** Because your **base permission is Read**, teams are the *only* way members get **Write/Maintain/Admin** access. Exactly what you want. 💪

---

## 🧯 Best Practices to Apply Right After Creating Teams

- Add repos to teams immediately (**Teams → Repositories → Add → set role**).
- **Branch protection rules** → require reviews from `@org/instructors` (and/or `@org/maintainers`).
- **CODEOWNERS** file → route PRs to the right team automatically:
  ```
  # .github/CODEOWNERS
  * @NakodTech-DevSecOps-Academy/instructors
  ```
- Use team mentions in issues/PRs: `@NakodTech-DevSecOps-Academy/instructors`  
- Nest teams (optional): **instructors** as parent; **linux**, **aws**, **security** as children.

---

## 🔍 Quick Verification

- Add a test user to **no teams** → confirm they only have **Read**.
- Add same user to **students** → they can push to lab repos but not elsewhere.
- Mention `@org/instructors` on a PR → team gets notified.

---

## 🧪 (Optional) API Example (for automation)

> Only if you prefer scripting; otherwise skip.

```bash
# Create a team (needs a PAT with admin:org)
curl -s -H "Authorization: Bearer $GH_TOKEN"   -H "Accept: application/vnd.github+json"   -X POST https://api.github.com/orgs/NakodTech-DevSecops-Academy/teams   -d '{"name":"instructors","privacy":"closed"}'
```
