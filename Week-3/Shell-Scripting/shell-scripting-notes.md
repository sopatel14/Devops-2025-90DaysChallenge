🚀 Week 3 Challenge 1: User Account Management
🧩 Challenge Description

In this challenge, you will create a bash script that provides options for managing user accounts on the system. The script should allow users to perform various user account-related tasks based on command-line arguments.

 Requirements
Part 1: Account Creation

Implement an option -c or --create that allows the script to create a new user account.
The script should:

Prompt the user to enter a new username and password.

Check if the username already exists.

If not, create the user and display a success message.

Part 2: Account Deletion

Implement an option -d or --delete that allows the script to delete an existing user account.
The script should:

Prompt the user to enter a username to delete.

Verify if the username exists.

Delete the account and display a confirmation message.

Part 3: Password Reset

Implement an option -r or --reset that allows the script to reset a user’s password.
The script should:

Prompt for username and new password.

Verify if the user exists.

Reset the password and confirm the change.

Part 4: List User Accounts

Implement an option -l or --list that displays all user accounts on the system along with their UIDs.

Part 5: Help and Usage Information

Implement an option -h or --help to show usage information and script options.

Bonus Points (Optional)

Display detailed user account information (home directory, shell, etc.).

Modify user properties (username, UID, etc.).

Handle all errors gracefully with user-friendly prompts.

 Solution: user_management.sh
#!/bin/bash
# ==========================================
# 🔹 User Management Script
# Author: Sourav Patel
# Description:
#   A bash script that manages user accounts
#   (create, delete, reset password, list, help)
# ==========================================

# --- Help Section ---
if [ "$1" = "-h" ] || [ "$1" = "--help" ]; then
    echo "Usage: $0 [OPTIONS]"
    echo "Options:"
    echo "  -c, --create   Create a new user account"
    echo "  -d, --delete   Delete an existing user account"
    echo "  -r, --reset    Reset password of an existing user"
    echo "  -l, --list     List all user accounts"
    echo "  -h, --help     Display this help message"
    exit 0
fi

# --- Create User Section ---
if [ "$1" = "-c" ] || [ "$1" = "--create" ]; then
    echo "Let's create a new username and set the password for the user"
    read -p "Please enter your new username: " username
    read -s -p "Please enter your password: " password
    echo

    # Check if user already exists
    if grep -q "^$username:" /etc/passwd; then
        echo "The user $username already exists."
        exit 1
    fi

    # Create user and set password
    sudo useradd -m "$username"
    echo "$username:$password" | sudo chpasswd
    echo "New user '$username' created successfully."
    exit 0
fi

# --- Delete User Section ---
if [ "$1" = "-d" ] || [ "$1" = "--delete" ]; then
    read -p "Please enter the username to delete: " username
    echo

    # Check if user exists
    if grep -q "^$username:" /etc/passwd; then
        sudo userdel -r "$username"
        echo "User '$username' deleted successfully."
    else
        echo "The user $username does not exist."
        exit 1
    fi
    exit 0
fi

# --- Reset Password Section ---
if [ "$1" = "-r" ] || [ "$1" = "--reset" ]; then
    read -p "Please enter the username to reset the password: " username
    read -sp "Please enter the new password: " password
    echo

    # Check if user exists
    if grep -q "^$username:" /etc/passwd; then
        echo "$username:$password" | sudo chpasswd
        echo "Password for '$username' reset successfully."
    else
        echo "The user $username does not exist."
        exit 1
    fi
    exit 0
fi

# --- List Users Section ---
if [ "$1" = "-l" ] || [ "$1" = "--list" ]; then
    echo "👥 Listing all users and their UIDs:"
    getent passwd | awk -F: '{ print "User:", $1, "| UID:", $3 }'
    exit 0
fi

# --- Default: Invalid Option ---
echo "Invalid option. Use -h or --help for usage info."
exit 1




Week 3 Challenge 2: Automated Backup & Recovery using Cron
🧩 Challenge Description

In this challenge, you will create a bash script that performs a backup of a specified directory and implements a rotation mechanism to manage backups.

 Requirements

Your task is to create a bash script that:

Takes a directory path as input.

Performs a timestamped backup of the directory.

Retains only the last 3 backups (deleting older ones).

Additionally, use Cron to automate the backup daily.

 Solution 1: backup_rotation.sh
#!/bin/bash
# ==========================================
# 🔹 Automated Backup & Rotation Script
# Author: Sourav Patel
# Description:
#   Creates timestamped backups of a directory
#   and keeps only the last 3 backups.
# ==========================================

# === Fixed Paths ===
src="/home/ubuntu/scripts"     # Source directory to backup
dest="/home/ubuntu/backups"    # Destination directory for backups

# === Step 1: Check if source exists ===
if [ ! -d "$src" ]; then
  echo "Error: Source directory '$src' does not exist."
  exit 1
fi

# === Step 2: Create destination if it doesn't exist ===
mkdir -p "$dest"

# === Step 3: Create a timestamp ===
timestamp=$(date '+%Y-%m-%d_%H-%M-%S')

# === Step 4: Define backup filename ===
backup_file="$dest/backup_$timestamp.zip"

# === Step 5: Create a ZIP backup ===
zip -r "$backup_file" "$src" >/dev/null 2>&1

# Check if backup succeeded
if [ $? -eq 0 ]; then
  echo "Backup created successfully: $backup_file"
else
  echo "Backup failed!"
  exit 1
fi

# === Step 6: Backup rotation (keep only last 3 backups) ===
cd "$dest" || exit
backups=( $(ls -t backup_*.zip 2>/dev/null) )

if [ ${#backups[@]} -gt 3 ]; then
  delete_count=$(( ${#backups[@]} - 3 ))
  echo "🧹 Removing $delete_count old backup(s)..."
  for old_backup in "${backups[@]:3}"; do
    rm -f "$old_backup"
    echo "Removed: $old_backup"
  done
else
  echo "No old backups to remove."
fi

echo "Backup rotation complete."

crontab -e

# Run automated backup at midnight every day
0 0 * * * /home/ubuntu/scripts/backup_rotation.sh >> /home/ubuntu/backup_log.txt 2>&1
