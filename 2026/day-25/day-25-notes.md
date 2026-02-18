What is the difference between --soft, --mixed, and --hard?
These options control what Git resets when you run: **git reset <option> <commit>**
--soft
Moves the branch pointer (HEAD) to a previous commit. Keeps changes in the staging area, keeps changes in the working directory. It only resets commit history.
Example: git reset --soft HEAD~1, Undo last commit but keep changes staged.
--mixed (default)
Moves the branch pointer (HEAD).Unstages changes, keeps changes in working directory.This is the default behavior if no option is specified.
Example: git reset HEAD~1, Undo last commit and unstage the changes.
--hard
Moves the branch pointer (HEAD). Deletes changes from staging area, deletes changes from working directory. Everything after that commit is permanently removed.
Example: git reset --hard HEAD~1, Completely removes last commit and its changes.

Which one is destructive and why?
--hard is destructive. Because it deletes: Commit history,Staged changes,Working directory changes. The changes cannot be recovered easily unless found in reflog.

When would you use each one?
Use --soft when:  We want to combine commits
                  We want to edit commit messages
                  We want to keep changes staged
Use --mixed when: We want to uncommit changes
                  We want to modify files before committing again
                  We want to unstage files
Use --hard when:  we want to completely discard changes
                  We want to match exactly a previous commit
                  We are cleaning up local experiments

Should you ever use git reset on commits that are already pushed?
No, we should not reset commits that are already pushed to a shared repository. Because it rewrites history, changes commit hashes, so it can causes conflicts for other team members,
it may require force pushing. Reset is safe only for local commits that have not been pushed.
If changes are already pushed, use: git revert, Instead of reset.

How is git revert different from git reset?
git reset moves the branch pointer (HEAD) backward,with this we can modify commit history, remove commits, rewrites history (especially with --hard)Example:
git reset --hard HEAD~1
This removes the last commit completely.
git revert does NOT delete commits, it creates a new commit that reverses the changes of a previous commit while preserving the historyExample:
git revert <commit-hash>, Git creates a new commit that undoes the selected commit.

Why is revert considered safer than reset for shared branches?
Revert is safer because tt does not rewrite history, does not change commit hashes, doesn't affect other developers' history
In shared branches (like main), rewriting history using reset can break other developers’ repositories. Revert keeps the history intact and transparent.

When would you use revert vs reset?
Use reset when we are working locally, the commits have NOT been pushed, we want to clean up history, made a mistake and want to undo it completely. In simple words use reset 
when working locally.
Use revert when we had already pushed the commits,working in a team or working on shared branches(main,production)and want to undo changes safely. In simple words code is already pushed.

Diff bw Feature : git reset && git revert 
 What it does? Moves HEAD to a previous commit and optionally modifies staging/working directory | Creates a new commit that undoes changes of a specific commit 
 Removes commit from history?  Yes | No 
 Safe for shared/pushed branches?  No | Yes 
 When to use?  When working locally and commits are not pushed | When working on shared branches or pushed commits

Which strategy would you use for a startup shipping fast?
For a startup shipping fast the preferred strategy is Squash Merge (or simple merge to main), bcz it keeps main clean and readable, avoids messy commit history. 
In this review process is faster, the workflow is simple with less process overhead. In Short: Clean, fast, minimal friction.
Startups optimize for: Speed > Perfect history
Often workflow is: feature branch → PR → squash merge → deploy

Which strategy would you use for a large team with scheduled releases?
For a large team the preferred Strategy is regular Merge (with merge commits) bcz it preserves full development history, keeps context of how features evolved,
the debugging is easy, better traceability, important for compliance and audits. Large teams optimize for:
Stability + Traceability > Simplicity
They may use:
Feature branches          Release branches       Hotfix branches      Structured merge commits
Sometimes they combine:
Rebase (locally) + Merge commit (into main)
