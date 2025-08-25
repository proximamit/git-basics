# What are the available options to revert the git commit pushed to the remote

> In Git, there are ***several ways*** to revert a **commit** already **pushed** to a **remote repository**
---
### 1. **`git revert`** 

- **Purpose:** Undo the *effects* of a commit without changing the commit history.
- **Used when:** We want to "undo" a change while preserving history (e.g., in shared/public branches like `main`).

```bash
git revert <commit-hash>
git push origin <branch-name>
```
> Creates a new commit that reverses the specified commit.
---
###  2. **`git reset`** 

- **Purpose:** Move the branch pointer to a different commit, optionally altering the working directory.
- **Used when:** We want to ***rewrite history*** (e.g., in a private branch or when we are okay forcing a push).

**Hard Reset** – Discard all changes after the commit

```bash
git reset --hard <commit-hash>
git push --force
```
---
###  3. **`git rebase -i` (Interactive Rebase)** 

- **Purpose:** Edit, delete, or squash commits in history.
-  **Used when:** We want fine-grained control over recent commits and are okay rewriting history.

```bash
git rebase -i <commit-hash>
# Edit the commit list (e.g., drop, reword)
git push --force
```
> Commonly used to clean up a series of recent commits.
---
### Summary

| Method            | Changes History?  | Keeps old commit? | Purpose                                                          |
| ----------------- | ----------------- | ----------------- | ---------------------------------------------------------------- |
| `git revert`      | No                | Yes               | Undo the effects of a commit without changing the commit history |
| `git reset`       | Yes               | No                | Move the branch pointer to a different commit (altering history) | 
| `git rebase -i`   | Yes               | No                | Edit, delete, or squash commits in history                       |

> For `reset` and `rebase`, we need to do force push
`git push --force` 

---
### Note

## Force push

A force push in git `git push --force` or `git push -f` pushes changes to a remote branch that rewrite its commit history, even if it conflicts with what's already on the remote. This operation **overwrites** the remote branch with our local version