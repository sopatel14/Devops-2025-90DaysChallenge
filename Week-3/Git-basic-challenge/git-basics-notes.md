This is a solution for Git basics


## 🔧 Git Commands Used (Tasks 1–4)

```bash
# Clone repository
git clone https://github.com/sopatel14/90DaysOfDevOps.git
cd 90DaysOfDevOps/2025/git/01_Git_and_Github_Basics

# Setup
mkdir week-4-challenge
cd week-4-challenge
git init

# File creation and first commit
echo "Name: Sourav Patel" > info.txt
git add info.txt
git commit -m "Initial commit: Add info.txt with introductory content"

# Set remote with PAT
git remote add origin https://sopatel14:<your-PAT>@github.com/sopatel14/90DaysOfDevOps.git
git branch -M main
git push -u origin main

# Check commit history
git log

# Branching
git branch feature-update
git switch feature-update
echo "Added learning goals." >> info.txt
git add info.txt
git commit -m "Feature update: Enhance info.txt with additional details"
git push origin feature-update

🌱 Why Branching Strategies Matter

Branching strategies are critical for managing code in collaborative environments. Here's why:

    Isolate Features and Fixes:
    Each developer works on their own branch, which isolates changes and avoids disturbing the main codebase.

    Facilitate Parallel Development:
    Multiple team members can work simultaneously on different features, increasing productivity.

    Reduce Merge Conflicts:
    When features are isolated, it’s easier to resolve conflicts during merges.

    Enable Effective Code Reviews:
    Pull requests allow for peer review before changes are merged, improving code quality and catching bugs early.

    Using clear naming (like feature/, bugfix/, hotfix/) and branching models (e.g., Git Flow or GitHub Flow) enhances team coordination and project organization.
