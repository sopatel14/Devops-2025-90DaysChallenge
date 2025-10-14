Here are all the commands used in for git basic challenhe

# Clone the forked repository from GitHub
git clone https://github.com/sopatel14/Devops-2025-90DaysChallenge.git

# Navigate into the project folder
cd devops_workspace/Devops-2025-90DaysChallenge

# Go to the correct subdirectory for the Git challenge
cd Git-basic-challenge

# Create a new directory for this week's challenge
mkdir week-3-challenge
cd week-3-challenge

# Initialize a new Git repository
git init

# Create and edit the info.txt file
vim info.txt  # (Added name and short intro)

# Add the file to the staging area
git add info.txt

# First commit
git commit -m "This is an initial commit, introduction"

# Set Git user details (if not set already)
git config --global user.name "sopatel14"
git config --global user.email "souravpatel65@gmail.com"

# Add remote (origin) using correct HTTPS URL
git remote add origin https://github.com/sopatel14/Devops-2025-90DaysChallenge.git

# Verify remote was added successfully
git remote -v

# Check current branch
git branch  # Output: master

# Set upstream and push the 'master' branch
git push --set-upstream origin master


❗ Initially, push failed due to missing authentication. Used PAT embedded in the remote URL to fix it.

# Update remote to use Personal Access Token (PAT)
git remote set-url origin https://sopatel14:<your-PAT>@github.com/sopatel14/Devops-2025-90DaysChallenge.git

# Push again
git push -u origin master

# View the commit log
git log


# Create a new branch
git branch feature-update

# Switch to the new branch
git switch feature-update
# OR: git checkout feature-update

# Modify info.txt with more details
vim info.txt

# Stage and commit the changes
git add info.txt
git commit -m "This is a second commit, feature update branch"

# Push the feature branch
git push origin feature-update


Git Advanced 

Git Stash
When to use git stash:
When you need to switch branches but have uncommitted work

When interrupted by urgent tasks/bugs

Before pulling remote changes to avoid conflicts

When you want to test something quickly without committing

git stash apply        # Applies stash but keeps it in stash list
git stash pop          # Applies stash AND removes it from stash list
git stash apply stash@{1}  # Apply specific stash
git stash pop stash@{1}    # Apply and remove specific stash



Cherry-Picking
How cherry-picking is used in bug fixes:
bash
# Example: Apply a hotfix from main to multiple release branches
git checkout release-1.0
git cherry-pick abc123   # Bug fix commit from main
git checkout release-1.1  
git cherry-pick abc123   # Same fix in different branch

Risks of cherry-picking:
Missing dependencies: Commit might rely on other commits

Duplicate commits: Can create same change with different hashes

Merge conflicts: When the target branch has diverged significantly

History fragmentation: Makes git log harder to follow

Merge vs Rebase
Difference:
bash
# Merge - creates merge commit, preserves history
git merge feature-branch

# Rebase - rewrites history, linear timeline
git rebase main


Best practices for rebasing:
Only rebase local branches - never rebase shared/public branches

Rebase before creating PRs - keeps history clean

Use git pull --rebase instead of regular pull

Avoid rebasing after pushing to remote


Branching Strategies in Companies
1. Git Flow
text
main ────┐
        │
develop ─┼─────┬── feature/login
        │     └── feature/payment
        │
        └───── release/1.2.0
               │
               └── hotfix/critical-bug
Pros: Structured, good for versioned releases
Cons: Complex, many long-lived branches

2. GitHub Flow
text
main ───┬── feature/auth
        ├── feature/ui-update
        └── hotfix/security-patch
Pros: Simple, fast, CI/CD friendly
Cons: Less structure for versioning

3. Trunk-Based Development
text
main ───┬── short-lived-feature (1-2 days)
        ├── another-short-feature
        └── hotfix
Pros: Enables continuous delivery, reduces merge conflicts
Cons: Requires strong testing culture









