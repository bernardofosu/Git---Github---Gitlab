# 🔐 GitHub Organization Hardening — Quick Steps

Follow these once to make sure any **member who isn’t on a team only has _Read_ access**. Teams and explicit repository grants will still **override** base permission (by design).

---

## ✅ One‑Time Steps

1. 🧭 **Go to:** **Org → Settings → Member privileges**
2. 🧰 **Base permissions** → **Read** (applies to all members not on teams)
3. 🚫 **Disable repository creation for members** (uncheck **Public** & **Private**)
4. 🍴 **Disable forking of private repositories**
5. 🗂️ **Projects base permissions** → **No access** (or **Read** if you must)
6. 🌐 **Pages creation** → **Private only** (block public sites)
7. 🤖 **Integration access requests (outside collaborators)** → **Off**
8. 🔒 **Admin repo permissions**  
   - 🔕 **Change visibility** → **Off**  
   - 🗑️ **Delete/transfer repos** → **Off**  
   - 🧹 **Delete issues** → **Off**
9. 👥 **Team creation** → **Off** (only **Owners** create teams)
10. 🧱 **Security basics (recommended)**: Require **2FA**, default new repos **Private**, add **branch protection**, and use **Teams** for every write/admin role.

---

## 🧾 Member Privileges — Exact Settings

| # | 🧩 **Area** | 🧭 **Where in UI** | ⚙️ **Set this** |
|---:|:--|:--|:--|
| 1 | 🔧 **Base permissions** | Settings → Member privileges → **Base permissions** | **Read** 🔍 |
| 2 | 🏗️ **Repository creation** | Member privileges → **Repository creation** | **Disabled** 🚫 (uncheck **Public** & **Private**) |
| 3 | 🍴 **Repository forking** | Member privileges → **Repository forking** | **Off** ⛔ for “Allow forking of private repositories” |
| 4 | 🗂️ **Projects base permissions** | Member privileges → **Projects base permissions** | **No access** 🚷 *(or **Read** 👀 if needed)* |
| 5 | 🌐 **Pages creation** | Member privileges → **Pages creation** | **Private only** 🔒 |
| 6 | 🤖 **Integration access requests** | Member privileges | **Off** ❌ for outside collaborators |
| 7 | 🔕 **Change repo visibility** | Member privileges → **Admin repository permissions** | **Off** ❌ |
| 8 | 🗑️ **Delete/transfer repos** | Member privileges → **Admin repository permissions** | **Off** ❌ |
| 9 | 🧹 **Issue deletion** | Member privileges → **Admin repository permissions** | **Off** ❌ |
|10 | 👥 **Team creation** | Member privileges → **Team creation rules** | **Off** 🔒 (Owners only) |

---

## 🎯 Outcome
**Members not on any team = Read‑only.** Owners and Teams you grant keep their write/admin powers. Outside collaborators get **no** extra privileges from base settings.

---

## 🧪 Quick Verification

- 👤 Log in as a member **not** in any team → you can **view** repos but **can’t push/create**.  
- 🛑 Try to **create a repo/team/site** → **blocked**.  
- 🛠️ Add the member to a **Team with Write/Admin** → pushing/admin works as expected.

---

ℹ️ Tip: Keep an **“Owners”** team small. Use separate **Write**, **Maintain**, and **Admin** teams per repo or product area to keep access auditable.
