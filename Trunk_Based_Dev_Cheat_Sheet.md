
# Trunk-Based Development Cheat Sheet

## 1. Get the Latest Main (a.k.a. Trunk)
1. **Switch to `main`**  
   ```bash
   git checkout main
   ```
2. **Pull the latest changes**  
   ```bash
   git pull origin main
   ```

> **Tip**: Always start new work from the up-to-date `main`.

---

## 2. Create a Short-Lived Feature Branch (Optional)
1. **Create and switch to a new branch**  
   ```bash
   git checkout -b feature/my-awesome-change
   ```
   
> **Why?** Even in TBD, short branches are common for isolating risky or more complex changes.

---

## 3. Make Your Changes
1. **Add and commit** (repeat as needed):  
   ```bash
   git add .
   git commit -m "Describe what changed"
   ```
2. **Push your branch**  
   ```bash
   git push -u origin feature/my-awesome-change
   ```
   
> **Commit often**. Smaller commits make it easier to track and revert if needed.

---

## 4. Keep in Sync with `main`
1. **Fetch new changes** from the remote  
   ```bash
   git fetch origin
   ```
2. **Merge or Rebase** `main` into your local branch  
   - **Merge** approach:  
     ```bash
     git merge origin/main
     ```
   - **Rebase** approach (alternative, keeps linear history):  
     ```bash
     git rebase origin/main
     ```
3. **Resolve any conflicts** and commit/resume as needed.

> **Pro Tip**: Sync daily or whenever `main` changes significantly. Avoid stale branches.

---

## 5. Merge Back to `main`
1. **(If you directly merge)**  
   - Switch to `main`  
     ```bash
     git checkout main
     ```
   - Merge your branch  
     ```bash
     git merge feature/my-awesome-change
     ```
   - Push to remote  
     ```bash
     git push origin main
     ```
2. **(If you use Pull Requests)**  
   - Open a PR from your feature branch to `main`.
   - Merge after review and passing CI tests.

> **Keep merges small and frequent** to maintain a stable trunk.

---

## 6. Clean Up (Optional)
- **Delete local branch** (once merged):  
  ```bash
  git branch -d feature/my-awesome-change
  ```
- **Delete remote branch** (if it was pushed):  
  ```bash
  git push origin --delete feature/my-awesome-change
  ```

> Keeping your branch list clean avoids clutter in your Git repo.

---

## Bonus Git Commands

- **Stash unfinished work** if you need to switch tasks quickly:  
  ```bash
  git stash
  ```
  *Then later recover stashed changes:*  
  ```bash
  git stash pop
  ```

- **Undo last commit** (if you haven’t pushed):  
  ```bash
  git reset --soft HEAD~1
  ```
  *This keeps your changes in the working directory but rewinds the commit.*

- **Revert a commit that’s already pushed** (creates a new “undo” commit):  
  ```bash
  git revert <commit-hash>
  ```

- **See your branch’s commit log**:  
  ```bash
  git log --oneline
  ```

- **Check what branch you’re on**:  
  ```bash
  git branch
  ```

---

## Workflow Summary

1. **Pull `main`** – Start fresh.  
2. **Create short branch** – (optional, but common)  
3. **Code, commit, push** – Small, frequent commits.  
4. **Merge/Rebase regularly** – Stay up-to-date with `main`.  
5. **Merge to `main`** – Or open a quick PR.  
6. **Delete old branch** – Keep your repo tidy.

**Goal**: Keep `main` stable and always releasable, integrate changes early and often, and avoid long-lived branches.

