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
