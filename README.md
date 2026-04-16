# Enterprise Git Workflow Project
-Step 1: Task 1 — Repository Initialization

-Create a new folder and initialize the repo:
-mkdir enterprise-git-workflow
-cd enterprise-git-workflow
-git init

-Create an initial commit on main (Git now defaults to main):
-echo "# Enterprise Git Workflow Project" > README.md
-git add README.md
-git commit -m "Initial commit: Add project README"

-Create the required branches:
-git branch develop
-git branch feature/login

-Push everything to GitHub (create a new public repo on GitHub first, then link it):
-git remote add origin https://github.com/anupamduttactg/enterprise-git-workflow.git
-git push -u origin main
-git push origin develop
-git push origin feature/login

-Step 2: Task 2 — Branching Workflow
-Switch to develop as the integration branch (common in real workflows):
-git checkout develop
-Create the additional branches:
-git checkout -b feature/payment
-git checkout -b feature/profile
-git checkout -b bugfix/login-error
-Make some changes and commits (example content):

-On feature/payment:
-echo "Payment module added" > payment.md
-git add payment.md
-git commit -m "feat: implement payment gateway integration"
-echo "Added tests" >> payment.md
-git add payment.md
-git commit -m "test: add unit tests for payment"

-On feature/profile:
-git checkout feature/profile
-echo "User profile feature" > profile.md
-git add profile.md
-git commit -m "feat: add user profile management"

-On bugfix/login-error:
-git checkout bugfix/login-error
-echo "Fixed login error" > bugfix.md
-git add bugfix.md
-git commit -m "fix: resolve login error on invalid credentials"

-One merge using merge strategy (e.g., merge a small feature into develop):
-Bashgit checkout develop
-git merge feature/profile --no-ff -m "merge: integrate user profile feature"
-This creates a merge commit (visible history of integration).
-One integration using rebase strategy (e.g., integrate bugfix cleanly):
-git checkout bugfix/login-error
-git rebase develop   # Rebase bugfix onto latest develop
-git checkout develop
-git merge bugfix/login-error --no-ff -m "merge: integrate login error bugfix"
-(Or push the rebased branch and create a Pull Request on GitHub.)

-Step 3: Task 3 — Commit History Management 

# Commit 1
-echo "v1" > payment.md
-git add payment.md
-git commit -m "WIP: start payment"

# Commit 2
-echo "v2" >> payment.md
-git add payment.md
-git commit -m "added stripe"

# Commit 3 (typo)
-echo "v3 fixx" >> payment.md
-git add payment.md
-git commit -m "fix typo"

# Commit 4
-echo "v4 tests" >> payment.md
-git add payment.md
-git commit -m "add basic tests"

# Commit 5
-echo "v5 docs" >> payment.md
-git add payment.md
-git commit -m "update documentation"

-Now perform interactive rebase:Bashgit rebase -i HEAD~5 In the editor that opens, you'll see something like:textpick abc1234 WIP: start payment
-pick def5678 added stripe
-pick ghi9012 fix typo
-pick jkl3456 add basic tests
-pick mno7890 update documentationChange it to (example):textreword abc1234 Initial payment implementation
-squash def5678 added stripe
-fixup ghi9012 fix typo          # or squash
-squash jkl3456 add basic tests
-fixup mno7890 update documentation
-reword → changes the commit message of the first commit.
-squash / fixup → combines the commit into the previous one (fixup discards the message, squash lets you edit).
-Save and close the editor.
-A second editor will open for the new combined commit message. Write a clean one:textfeat: implement payment gateway with tests and docsSave and close. Your history is now clean (usually 1–2 commits instead of 5).
-(Optional but good) Force-push the cleaned branch if already pushed:git push origin feature/payment --force-with-lease

# Merge vs Rebase:
-Merge creates a new merge commit that preserves the full history and branch structure. It's safer for shared branches (like develop → main). It shows when and how features were integrated.
-Rebase replays your commits on top of another branch, creating a linear history. Better for cleaning private feature branches before merging. It rewrites history, so avoid on shared branches.
# Squash & Reword:
-Squash combines multiple small commits into one meaningful commit (keeps history clean).

