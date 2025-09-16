# 🧩 GitHub Onboarding — Action Notes

## 👥 Invite your first member
- **Why:** start collaboration while keeping least-privilege.
- **UI path:** **Org → People → Invite member**  
- **Do:**
  - Enter GitHub username/email → role **Member** (avoid Owner).  
  - Add them to the right **Team(s)** so they inherit repo access.  
  - Verify they can **read** but not push unless on a write team.  
- **Tip:** Require **2FA** for the org.

---

## 🔀 Create a pull request (PR)
- **Why:** reviews, audit trail, safer merges.
- **Flow:**
  1. Create branch: `feature/short-desc`
  2. Commit small, clear messages.
  3. **Open PR** → add description, screenshots if UI, link issues.
  4. **Request reviewers** (e.g., `@org/instructors`)  
  5. Address comments → **merge** (Squash or Merge Commit per policy) → delete branch.
- **Extras:** Add **PR template** (`.github/pull_request_template.md`) + **branch protection** (require reviews, status checks).

---

## 🤖 Auto-assign new issues
- **Why:** instant triage to keep backlog moving.
- **Two easy options:**
  - **Built-in “Auto-assign new issues” workflow** → **Repo → Actions → New workflow → Automation** → enable.
  - Or a minimal custom Action:
    ```yaml
    name: Auto-assign issues
    on:
      issues:
        types: [opened]
    permissions:
      issues: write
    jobs:
      assign:
        runs-on: ubuntu-latest
        steps:
          - uses: actions-ecosystem/action-add-assignees@v1
            with:
              assignees: "user1,user2"
    ```
- **Tip:** Use **labels** (e.g., `area/linux`, `good-first-issue`) + **Projects** for triage.

---

## 🧪 Run a continuous integration test (CI)
- **Why:** catch failures before merge; build trust in PRs.
- **Quick start (choose one):**

  **Python**
  ```yaml
  name: CI (Python)
  on: [push, pull_request]
  jobs:
    test:
      runs-on: ubuntu-latest
      steps:
        - uses: actions/checkout@v4
        - uses: actions/setup-python@v5
          with: { python-version: "3.11" }
        - run: pip install -r requirements.txt
        - run: pytest -q
  ```

  **Node.js**
  ```yaml
  name: CI (Node)
  on: [push, pull_request]
  jobs:
    test:
      runs-on: ubuntu-latest
      steps:
        - uses: actions/checkout@v4
        - uses: actions/setup-node@v4
          with: { node-version: "20" }
        - run: npm ci
        - run: npm test --silent
  ```

- **Tip:** Protect the default branch to **require CI to pass** before merging.

---

## ✅ Quick checklist
- [ ] Invite first member and add to correct **Team(s)**
- [ ] Create first **PR** from a feature branch
- [ ] Enable **Auto-assign issues** (and labels)
- [ ] Add a **CI** workflow and make it a required check
