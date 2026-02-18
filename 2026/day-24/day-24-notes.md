What is a fast-forward merge?
A fast-forward merge happens when the target branch has not moved ahead since the new branch was created. In this case, Git simply moves the branch pointer forward. There is no new
merge commit created. Example: We create feature-login from main, commit changes in feature-login, main has no new commits. We merge feature-login into main
Git just moves main forward to the latest commit of feature-login. History remains linear.

When does Git create a merge commit instead?
Git creates a merge commit when both branches have new commits after they diverged. Example: Create feature-login from main, Add commits to feature-login
Add a different commit to main, Now merge feature-login into main
Since both branches moved forward independently, Git cannot just move the pointer, it creates a new commit called a merge commit that combines both histories.
This keeps track of the fact that two development lines were merged.

What is a merge conflict?
A merge conflict happens when Git cannot automatically decide which changes to keep. This usually happens when:the same file, the same line, Is modified differently in two branches
Git stops the merge and asks you to manually resolve the conflict.

What does rebase actually do to your commits?
Rebase moves your branch to start from a new base commit. It takes your commits, temporarily removes them, moves the branch to the latest version of another branch (usually main), 
and then re-applies your commits on top of it. In simple terms rebase rewrites history.Example:
Before rebase:          main: A --- B --- C, feature: D --- E
After running:          git rebase main
History becomes:        main: A --- B --- C, feature: D' --- E'

How is the history different from a merge?
Merge: Keeps original commit history, Creates a merge commit, History may look branched
Example:  A --- B --- C
          \
          D --- E
          \
          M (merge commit)
History shows the branch structure.
Rebase: Rewrites commits, No merge commit, Creates a clean, linear history
A --- B --- C --- D' --- E'
It looks like all work happened sequentially.

Why should you never rebase commits that have been pushed and shared with others?
Because rebase changes commit history. When we rebase commit hashes change, history is rewritten.If others already pulled the old commits, their history will not match ours.
So it creates confusion and conflicts and can break collaboration.
Rule: Never rebase public/shared branches. Only rebase local branches that only you are using.

When would you use rebase vs merge?
We should use rebase when cleaning up local commits and updating your feature branch with latest main, and we want a clean linear history thi is recommended when one is working alone 
on branch. Example: git checkout feature, git rebase main
We should use merge when working in a team, merging completed features into main, We want to preserve history and the branch is already shared. Example:
git checkout main, git merge feature

What does squash merging do?
Squash merging combines all commits from a branch into a single commit before merging it into the target branch. Instead of preserving every individual commit, Git compresses them into
one clean commit. Example: Feature branch commits:
A --- B --- C (feature branch)
After squash merge into main:
main: X --- Y --- Z --- S
Where:
S = One single commit containing all changes from A, B, and C.
It creates a cleaner commit history.

When would you use squash merge vs regular merge?
Use **squash merge** when the feature branch has many small commits. Commits are messy (e.g., "fix", "typo", "update again"). We want clean and simple history in main, while working on
small features or bug fixes.It keeps main history easy to read.
Use **regular merge** when we want to preserve detailed commit history, working on large features, multiple developers contributed, we want to track development steps. Regular merge 
keeps the full history and shows how work evolved.

What is the trade-off of squashing?
The trade-off is we lose detailed commit history. After squashing we cannot see individual commits from the feature branch. Debugging specific intermediate changes becomes harder
Blame history becomes less detailed. So:
Squash = clean history but less detail
Regular merge = detailed history but possibly messy

What is the difference between git stash pop and git stash apply?
Both commands restore changes that were saved using git stash. Simple Difference **apply** → restore but keep stash, **pop** → restore and delete stash
**git stash apply**: Restores the stashed changes, keeps the stash in the stash list, it can be applied multiple times. Example: git stash apply
The changes come back, but the stash still exists.
**git stash pop**: Restores the stashed changes, removes the stash from the stash list, Example: git stash pop
The changes come back, and the stash entry is deleted.

When would you use stash in a real-world workflow?
We use stash when we have unfinished changes but need to switch context quickly. Real-world example:
We are working on a feature and suddenly, production has a bug. So we need to switch branches immediately but my working directory has uncommitted changes. Instead of committing 
incomplete work:  git stash
                  git checkout main
After fixing the issue, We return:  git checkout feature-branch
                                    git stash pop
Stash is useful for temporary work that is not ready to commit.

What does cherry-pick do?
Git cherry-pick takes a specific commit from one branch and applies it to another branch. It copies a single commit instead of merging the whole branch.
Example:  git cherry-pick <commit-hash>
This creates a new commit in the current branch with the same changes.

When would you use cherry-pick in a real project?
We should use cherry-pick when a bug fix in one branch needs to be applied to another branch, we want one specific commit, not the whole branch
We maintain multiple release branches. Example:
A bug is fixed in develop and production branch main also needs that fix, so instead of merging all changes, we cherry-pick only the bug fix commit

What can go wrong with cherry-picking?
It may lead to the same changes existing in multiple places, making tracking harder. Cherry-pick should be used carefully, not as a replacement for proper branching strategy.
Cherry-picking can cause:
Merge conflicts
Duplicate commits
Confusing history
Maintenance issues if done frequently



