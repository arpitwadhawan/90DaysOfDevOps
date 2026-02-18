What is a branch in Git?
A branch is an independent line of development.It is simply a pointer to a specific commit in the repository. When we create a branch, git creates a new pointer that can
move forward separately from other branches. Each branch allows you to work on changes without affecting other branches.By default, Git creates a branch called main.

Why do we use branches instead of committing everything to main?
We use branches to develop features safely, fix bugs without breaking stable code, experiment without risk, work in teams without conflicts.If everyone committed directly to main:
the main branch could break easily, bugs would affect production, feature development would be messy,branches keep work isolated until it's ready to merge.
Example workflow:
main → stable production code
feature-login → new feature

What is HEAD in Git?
HEAD is a pointer that tells Git, "Where we are currently?", It usually points to the latest commit on the current branch.
For example: If we are on main, HEAD points to the latest commit on main, If we switch to feature-login, HEAD moves to that branch,We can see your current branch with: git branch
The branch with * is where HEAD is pointing.

What happens to your files when you switch branches?
We use switch, when we want to change the branch on which we currently are. When we switch branches using:
git checkout branch-name
Git updates our working directory to match the snapshot of that branch.That means files may change, Some files may disappear or appear, our project instantly becomes
the version stored in that branch. However If we have uncommitted changes, Git may prevent switching to avoid data loss.

What is the difference between clone and fork?
In simple words clone means copy repository to your local machine and fork means copy repository to your GitHub account
Clone: git clone creates a local copy of a repository on your computer.It downloads all commits, branches, full history. After cloning, we can start working locally,
clone happens on our local machine. Example: git clone https://github.com/user/repo.git
Fork: a fork creates a copy of someone else's repository under your own GitHub account, it is done on GitHub, not on your local machine.
After forking we get our own copy of the repo, modify it freely, it does not affect the original project, Fork happens on GitHub.

When would you clone vs fork?

We use clone when:
We are part of the team
We have direct access to the repository
We want to work locally on your own or company project

We use fork when:
We want to contribute to someone else's project
We do not have write access to the original repository
We are contributing to open-source

After forking, how do you keep your fork in sync with the original repo?

When we fork a repository, our copy becomes independent, to sync it with the original repository:
Step 1: Add original repo as upstream
git remote add upstream https://github.com/original-owner/repo.git
Step 2: Fetch changes from upstream
git fetch upstream
Step 3: Merge changes into your main branch
git checkout main
git merge upstream/main
Now your fork is updated with the latest changes. While on github there is an option to fork sycn, on click it get synced.



