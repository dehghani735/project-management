# Scrum

## Guidelines
To prepare for Java developer interviews using *The Professional Scrum Team* by Kurt Bittner, you can focus on these key areas:

### 1. **Scrum Framework and Roles**
   - Understand Scrum roles deeply (Product Owner, Scrum Master, Developers).
   - Be prepared to explain how a developer collaborates with these roles within a Scrum team.
   - Practice describing scenarios where clear role definition helped in delivering value or resolving team conflicts.

### 2. **Cross-Functional Collaboration**
   - Emphasize how you, as a Java developer, can contribute to a cross-functional team.
   - Highlight examples where you've taken on tasks outside of coding, such as assisting with testing, documentation, or infrastructure.
   - Show adaptability in working with non-technical roles like Product Owners or stakeholders.

### 3. **Commitment to Continuous Improvement**
   - Discuss how you approach feedback and retrospectives. Be ready to provide examples where retrospective feedback led to a tangible improvement.
   - Illustrate your commitment to continuous learning, mentioning technical skills you've developed to support the team’s goals.

### 4. **Focus on Delivering Incremental Value**
   - Describe how you prioritize your tasks and ensure that your work aligns with the Sprint goals.
   - Share instances of how you’ve contributed to delivering increments of potentially shippable code, and how you ensure quality within these increments.

### 5. **Handling Technical Debt and Code Quality**
   - Highlight your approach to managing technical debt in an Agile context and balancing it with delivery speed.
   - Discuss how you maintain code quality through practices like code reviews, automated testing, and pair programming.

### 6. **Ownership and Accountability**
   - Prepare to discuss how you take ownership of tasks and are accountable for outcomes.
   - Explain how you manage work when facing unclear requirements or changing priorities, a common scenario in Agile development.

These guidelines will show your ability to work effectively within a Scrum team and how your Java development expertise contributes to Scrum practices and team goals.



# Git Flow
In Git, rolling back changes depends on whether they have been **committed** or not. Below, I'll explain how to handle both cases.

---

## **1. Rolling Back Uncommitted Changes**

These are changes that are either in the **working directory** or **staging area** but have not been committed yet.

### A. **Undo Changes in the Working Directory** (Not Staged)

To revert changes made to a file before staging (i.e., changes that exist in the working directory but are not yet staged):

```bash
git restore <filename>
```

If you want to revert changes to all files:

```bash
git restore .
```

This will discard all changes in the working directory and revert the file(s) to their last committed state.

### B. **Undo Changes in the Staging Area** (Staged but Not Committed)

If the changes have been staged (i.e., added to the staging area using `git add`) but not yet committed, you can unstage them without losing your changes:

```bash
git restore --staged <filename>
```

If you want to unstage all files:

```bash
git restore --staged .
```

This moves the changes back to the working directory, so the changes are still there, but they are no longer staged for the next commit.

---

## **2. Rolling Back Committed Changes**

If you've already committed changes, there are several ways to undo or roll back those commits. The method you choose depends on whether you've pushed those changes to a remote repository or not.

### A. **Undo the Last Commit (Before Pushing)**

If you want to undo the last commit but keep the changes in your working directory (i.e., you want to "uncommit" but not lose the changes):

```bash
git reset --soft HEAD~1
```

- `--soft`: This option keeps the changes in the staging area, so you can edit them and recommit.
- `HEAD~1`: Refers to the last commit.

If you want to undo the last commit **and discard the changes**:

```bash
git reset --hard HEAD~1
```

- `--hard`: This will remove the last commit **and** all changes made in that commit from your working directory.

### B. **Undo Multiple Commits**

To undo several commits, specify how many commits to go back:

```bash
git reset --soft HEAD~n
```

Where `n` is the number of commits you want to undo.

If you want to discard changes and commits:

```bash
git reset --hard HEAD~n
```

### C. **Reverting a Commit (Safe for Pushed Commits)**

If you've already pushed the commit to a remote repository and want to undo it **without rewriting history**, you should use `git revert`. This creates a new commit that undoes the changes made in the specified commit, without altering the commit history.

To revert a single commit:

```bash
git revert <commit-hash>
```

This will create a new commit that reverses the changes introduced by `<commit-hash>`.

To revert multiple commits:

```bash
git revert <commit-hash>^..<latest-commit-hash>
```

### D. **Undo a Pushed Commit with `git reset` (Force Push)**

If you've already pushed the commit but still want to undo it, and **you are sure you want to rewrite the history**, you can reset and force push:

```bash
git reset --hard HEAD~1
git push --force
```

⚠️ **Warning**: This approach is dangerous if others have already pulled from the repository, as it rewrites history and can cause conflicts. Use with caution.

---

### Summary Table:

| Situation                              | Command                                      |
|----------------------------------------|----------------------------------------------|
| Discard uncommitted changes (not staged)  | `git restore <filename>` or `git restore .`   |
| Unstage changes (but keep in working directory) | `git restore --staged <filename>` or `git restore --staged .` |
| Undo last commit, keep changes staged  | `git reset --soft HEAD~1`                    |
| Undo last commit, discard changes      | `git reset --hard HEAD~1`                    |
| Revert a pushed commit (safe)          | `git revert <commit-hash>`                   |
| Undo a pushed commit (force push)      | `git reset --hard HEAD~1` + `git push --force` |

This guide should help you handle various scenarios of rolling back changes in Git depending on whether the changes are committed, staged, or pushed!



`git stash` is another useful tool in Git to temporarily save uncommitted changes without committing them. It's commonly used when you want to switch branches or pull in new changes but don’t want to commit your current work yet. Here's how `git stash` works and how it compares to other rollback methods.

### What is `git stash`?

`git stash` temporarily shelves (or "stashes") changes in your working directory and staging area. This lets you clean your working directory without committing your changes. You can then later reapply these changes when you're ready to continue working on them.

---

### Basic `git stash` Commands

#### 1. **Stash Your Changes**

To save your changes (both staged and unstaged) into a "stash" and reset the working directory to the latest commit, run:

```bash
git stash
```

By default, `git stash` stashes both staged and unstaged changes but leaves untracked files alone.

If you also want to stash untracked files (new files not yet added with `git add`), you can use:

```bash
git stash --include-untracked
```

You can give the stash a custom message to identify it later:

```bash
git stash save "My WIP changes"
```

#### 2. **Apply Stashed Changes**

When you're ready to bring the changes back into your working directory, use:

```bash
git stash apply
```

This reapplies the most recent stash, but it leaves the stash in the stash list (i.e., it doesn’t delete the stash).

If you want to apply and remove the stash (i.e., remove the stash from the stash list):

```bash
git stash pop
```

#### 3. **View the Stash List**

To see all the stashes you have saved:

```bash
git stash list
```

You'll see a list of stashed changes, e.g.:

```
stash@{0}: WIP on master: 123abc Adding new feature
stash@{1}: WIP on dev: 456def Fixing a bug
```

#### 4. **Apply a Specific Stash**

If you have multiple stashes and want to apply a specific one, you can refer to the stash index:

```bash
git stash apply stash@{1}
```

This applies the second stash in the list (`stash@{1}`).

#### 5. **Drop/Delete a Stash**

If you no longer need a specific stash, you can remove it from the stash list:

```bash
git stash drop stash@{0}
```

If you want to delete **all** stashes:

```bash
git stash clear
```

---

### Using `git stash` in Different Scenarios

#### A. **Switching Branches Temporarily**

Imagine you're working on a feature in the `dev` branch but need to switch to `master` to pull the latest changes or fix a quick bug. Instead of committing your incomplete work, you can stash the changes:

```bash
git stash
git checkout master
```

After fixing the bug or pulling changes, you can switch back to `dev` and reapply your stashed work:

```bash
git checkout dev
git stash pop
```

#### B. **Stashing Specific Files**

If you only want to stash certain files (instead of all changes), you can specify files like this:

```bash
git stash push <filename>
```

For example:

```bash
git stash push index.html
```

#### C. **Stashing Changes for a Clean Pull**

If you’re about to pull in new changes but have uncommitted work, it's better to stash them first to avoid merge conflicts:

```bash
git stash
git pull
git stash pop
```

---

### Comparison: `git stash` vs `git reset` vs `git restore`

| Use Case                          | `git stash`                                                                 | `git reset`                                  | `git restore`                                     |
|------------------------------------|-----------------------------------------------------------------------------|----------------------------------------------|---------------------------------------------------|
| Temporarily save uncommitted work  | Temporarily stores your work and allows you to apply it later.               | Resets the commit history (for committed changes). | Restores files to their state in the last commit. |
| Reapply changes later              | Yes, you can stash and reapply as needed.                                    | Not suitable for temporarily saving changes.  | No, it directly discards changes.                 |
| Switch branches                    | Yes, you can stash and switch branches without committing.                   | No, resetting will lose changes unless committed. | No, restore only works within the same branch.    |
| Stash both staged & unstaged files | Yes, by default. You can also stash untracked files with `--include-untracked`. | N/A                                          | N/A                                               |
| Revert to last commit              | No, it’s only for temporary saving.                                          | `git reset --hard` discards all changes.      | `git restore` can reset working directory changes.|

---

### Summary

- **`git stash`** is useful when you want to temporarily save your uncommitted work to come back to it later. It’s ideal for situations where you need a clean working directory but don’t want to commit incomplete changes.
- **`git reset`** is used to undo commits, but it should be used carefully when dealing with pushed commits.
- **`git restore`** is for discarding changes either in the working directory or staging area, but doesn’t keep them for later use.

`git stash` is a great tool when you need flexibility to store uncommitted work while working on other tasks or switching branches.