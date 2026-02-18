Difference between git add and git commit:
git add moves changes from the working directory into the staging area, git commit saves the staged changes permanently into the 
repository with a message.We can add multiple times before committing once.
git add = "Prepare these changes"
git commit = "Record these changes in history"
Example 
git add file.txt
git commit -m "Added new feature"

Staging Area:
The staging area acts as a preparation zone before a commit. It allows you to choose exactly which changes to include and exclude unwanted
changes. Without a staging area every change would be committed immediately we couldn’t separate features or fixes cleanly. The staging 
area gives us control and precision.

Git Log:
git log shows the commit history. It displays commit hash (unique ID), author name, date,commit message
Example output:
commit a1b2c3d4
Author: Arpit
Date:   Feb 18, 2026
    Added login feature
We can also use git log --oneline, for compact history view.

.git
The .git/ folder stores all Git metadata. It contains commit history, branch information, configuration,objects and references
If we delete the .git/ folder, the project stops being a Git repository all commit history is lost, Git commands will no longer work.
Our code files remain, but version control is gone.

Dfference between a working directory, staging area, and repository
Working Directory: Where we edit files. These changes are not yet tracked by Git.
Staging Area: A temporary area where selected changes are prepared for commit.
Repository: The permanent storage of committed changes inside .git/.
it is like this
Working Directory → Staging Area → Repository
Edit → Select → Save to history


