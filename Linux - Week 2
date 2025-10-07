# 🧑‍💻 Week 2: Linux System Administration & Automation  
**90 Days of DevOps – 2025 Edition**

This week focused on mastering **Linux system administration and automation** through hands-on exercises such as user management, permissions, log analysis, volume mounts, process control, and scripting.

---

## 🚀 Project Overview
**Scenario:**  
You are managing a Linux-based production server and need to ensure that users, logs, and processes are well-maintained.  
This project covers:  
- User and Group Management  
- File Permissions  
- Log Analysis  
- Volume & Disk Management  
- Process Monitoring  
- Automation via Shell Scripting  

---

## 🧩 Task 1: User & Group Management

### 🧱 Create a User
```bash
sudo useradd -m devops_user
````

| Command   | Description                                  |
| --------- | -------------------------------------------- |
| `useradd` | Creates a new user                           |
| `-m`      | Creates a home directory `/home/devops_user` |

---

### 👥 Create a Group

```bash
sudo groupadd devops_team
```

| Command    | Description                             |
| ---------- | --------------------------------------- |
| `groupadd` | Creates a new group named `devops_team` |

---

### 🔗 Add User to the Group

```bash
sudo gpasswd -a devops_user devops_team
```

| Command                     | Description                       |
| --------------------------- | --------------------------------- |
| `gpasswd -a <user> <group>` | Adds the user to a specific group |

---

### 🔐 Set User Password

```bash
sudo passwd devops_user
```

| Command  | Description                              |
| -------- | ---------------------------------------- |
| `passwd` | Prompts to set or update a user password |

---

### 🛠️ Grant Sudo Privileges

```bash
sudo gpasswd -a devops_user sudo
```

| Command           | Description                                        |
| ----------------- | -------------------------------------------------- |
| `sudo gpasswd -a` | Adds the user to the `sudo` group for admin rights |

---

### 🚫 Restrict SSH Login for Specific Users

```bash
sudo vim /etc/ssh/sshd_config
```

Add this line at the bottom:

```
DenyUsers shubham
```

Then verify:

```bash
sudo sshd -t
sudo grep "DenyUsers" /etc/ssh/sshd_config
```

| File/Command           | Description                               |
| ---------------------- | ----------------------------------------- |
| `/etc/ssh/sshd_config` | Main SSH configuration file               |
| `DenyUsers`            | Restricts SSH login for listed users      |
| `sshd -t`              | Tests SSH configuration for syntax errors |

---

## 📂 Task 2: File & Directory Permissions

### 📁 Create Workspace and File

```bash
mkdir /devops_workspace
cd /devops_workspace
vim project_notes.txt
```

### ⚙️ Set Permissions

```bash
chmod 740 project_notes.txt
```

| Code | Permission | Meaning                        |
| ---- | ---------- | ------------------------------ |
| `7`  | rwx        | Owner can read, write, execute |
| `4`  | r--        | Group can read                 |
| `0`  | ---        | Others have no access          |

Verify:

```bash
ls -l
```

Output Example:

```
-rwxr----- 1 sourav devops_team 0 Oct 7 10:32 project_notes.txt
```

---

## 🧾 Task 3: Log File Analysis (grep, awk, sed)

Download `Linux_2k.log` from [LogHub GitHub Repo](https://github.com/logpai/loghub).

---

### 🔍 Find All “Error” Entries

```bash
grep -i "authentication failure" Linux_2k.log
```

| Option | Description                         |
| ------ | ----------------------------------- |
| `grep` | Searches for specific text in files |
| `-i`   | Ignores case while searching        |

---

### 🕓 Extract Timestamps & Log Level

```bash
awk '/authentication failure/ {print $1, $2, $3, $4}' Linux_2k.log
```

| Command                  | Description                                              |
| ------------------------ | -------------------------------------------------------- |
| `awk`                    | Text-processing utility                                  |
| `{print $1, $2, $3, $4}` | Prints first four fields (usually date/time + log level) |

---

### 🧹 Replace IP Addresses with [REDACTED]

```bash
sed -E 's/rhost=([0-9]{1,3}\.){3}[0-9]{1,3}/rhost=[REDACTED]/g' Linux_2k.log
```

| Symbol/Option             | Description                          |
| ------------------------- | ------------------------------------ |
| `sed`                     | Stream editor for text substitution  |
| `-E`                      | Enables extended regular expressions |
| `s/pattern/replacement/g` | Substitutes all matching text        |

---

### 🏆 Find Most Frequent Log Entries

```bash
sort Linux_2k.log | uniq -c | sort -nr | head -10
```

| Command    | Description                        |
| ---------- | ---------------------------------- |
| `sort`     | Sorts lines alphabetically         |
| `uniq -c`  | Counts unique entries              |
| `sort -nr` | Sorts numerically in reverse order |
| `head -10` | Displays top 10 results            |

---

## 💾 Task 4: Volume Management & Disk Usage

### 📁 Create Mount Directory

```bash
sudo mkdir /mnt/devops_data
```

### 💽 Create Virtual Disk Image (Loop Device)

```bash
sudo dd if=/dev/zero of=/tmp/devops_data.img bs=1M count=1024
```

| Parameter                 | Description                     |
| ------------------------- | ------------------------------- |
| `if=/dev/zero`            | Input file providing zero bytes |
| `of=/tmp/devops_data.img` | Output image file               |
| `bs=1M`                   | Block size of 1 MB              |
| `count=1024`              | Total of 1 GB data              |

---

### 🔗 Mount the Image

```bash
sudo mount -o loop /tmp/devops_data.img /mnt/devops_data
```

| Option    | Description                           |
| --------- | ------------------------------------- |
| `-o loop` | Mounts file as a virtual block device |

Verify:

```bash
df -h
mount | grep devops_data
```

---

## ⚙️ Task 5: Process Management & Monitoring

### ▶️ Start Background Process

```bash
ping google.com > ping_test.log &
```

| Symbol | Description                |
| ------ | -------------------------- |
| `>`    | Redirects output to file   |
| `&`    | Runs process in background |

---

### 🔍 Monitor Process

```bash
ps aux | grep ping
```

| Command     | Description                         |
| ----------- | ----------------------------------- |
| `ps aux`    | Displays all running processes      |
| `grep ping` | Filters processes containing “ping” |

---

### 🛑 Kill the Process

```bash
kill <process_id>
```

| Command | Description                       |
| ------- | --------------------------------- |
| `kill`  | Terminates a process using its ID |

Verify process termination:

```bash
ps aux | grep ping
```

---

## 🧠 Task 6: Automate Backups with Shell Scripting

### 📝 Create Script: `do-backup.sh`

```bash
#!/bin/bash
echo "Backup started"

# Ensure destination directory exists
sudo mkdir -p /backups

# Create compressed backup with date
sudo tar -czf /backups/backup_$(date +%F).tar.gz /home/sourav/devops_workspace

# Verify backup success
if [ $? -eq 0 ]; then
    echo -e "\e[32mBackup successful!\e[0m"
else
    echo -e "\e[31mBackup failed!\e[0m"
fi
```

| Component     | Description                          |
| ------------- | ------------------------------------ |
| `tar -czf`    | Creates compressed `.tar.gz` archive |
| `$(date +%F)` | Inserts current date (YYYY-MM-DD)    |
| `$?`          | Checks exit status of last command   |
| `\e[32m`      | Prints text in green color           |

Run the script:

```bash
chmod +x do-backup.sh
./do-backup.sh
```

Verify:

```bash
ls -lh /backups
```

Example output:

```
-rw-r--r-- 1 root root 2.5K Oct 7 14:37 backup_2025-10-07.tar.gz
```

---

## 🪶 Extra Task: Extract ERROR & WARNING Logs

### 🧰 Script: `extract-logs.sh`

```bash
#!/bin/bash
echo "Extracting ERROR and WARNING logs from Linux_2k.log..."

grep -E "ERROR|WARNING" /home/sourav/Downloads/Linux_2k.log | \
awk '{print $1,$2,$3,$4,$5,$6,$7,$8,$9,$10,$11,$12,$13,$14}' | uniq

echo "✅ Logs extracted successfully."
```

| Tool      | Description                                         |
| --------- | --------------------------------------------------- |
| `grep -E` | Searches using extended regex for multiple patterns |
| `awk`     | Extracts and formats specific columns               |
| `uniq`    | Removes duplicate lines                             |

---

## ✅ Summary

This week covered:

* 👥 User & Group Management
* 🗂️ File Permissions
* 🧾 Log Analysis with `grep`, `awk`, `sed`
* 💽 Volume Management
* ⚙️ Process Control
* 🧠 Shell Script Automation

Each task strengthened my Linux fundamentals — crucial for every DevOps professional.

