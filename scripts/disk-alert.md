# 💾 Disk Usage Alert Script (Bash)

This project contains a **simple yet powerful Bash script** that monitors disk usage for a specific directory.  
If disk usage **crosses a defined limit**, the script **automatically sends an email alert**.

This project is specially designed for **freshers and Linux beginners** to understand real-world monitoring and alerting using Bash scripting.

---

## 📌 What This Script Does

- Monitors disk usage for **/mnt/app-data**
- Extracts disk usage percentage
- Compares usage against a **33% threshold**
- If usage is:
  - ❌ **Greater than or equal to 33%** → Sends an **email alert**
  - ✅ **Below 33%** → Displays a safe status message

---

## 🎯 Why This Script Is Useful

- Prevents disk full issues
- Helps in proactive system monitoring
- Reduces manual checks
- Helps freshers learn:
  - Disk monitoring with `df`
  - Text filtering using `grep`, `awk`, `tr`
  - Conditional logic (`if-else`)
  - Sending emails from Bash
- Great **Linux mini project** for resumes and GitHub

---

## 🧠 Prerequisites

Before running this script, make sure:

- You are using a **Linux system**
- The directory `/mnt/app-data` exists
- Disk space can be read using `df`
- Mail service (`mail` or `mailx`) is installed and configured
- Internet / SMTP access is available for email alerts

---

## 🔍 How the Script Works (Step-by-Step)

1. Script starts using the **Bash shell**
2. Disk usage of `/mnt/app-data` is fetched using `df`
3. Header line is removed for clean output
4. Usage percentage is extracted
5. `%` sign is removed to allow numeric comparison
6. Disk usage is compared with **33%**
7. If threshold is exceeded:
   - Email alert is sent
8. Otherwise:
   - Normal usage message is displayed

---

**📋 COMMAND EXPLANATION TABLE (FOR FRESHERS)**


| Command / Syntax           | Description                                   | Why It Is Used                          |
|---------------------------|-----------------------------------------------|-----------------------------------------|
| !/bin/bash                | Specifies Bash as the script interpreter.     | Ensures the script runs using Bash.     |
| df -h /mnt/app-data       | Displays disk usage for the mount point.      | Checks space usage of target directory. |
| grep -v "Filesystem"      | Removes the header line from df output.       | Keeps output clean for processing.      |
| awk '{print $5}'          | Extracts the 5th column (usage percentage).   | Retrieves disk usage value.             |
| tr -d '%'                 | Removes the % symbol from output.             | Enables numeric comparison.             |
| space=$(...)              | Stores command output in a variable.          | Used for conditional logic.             |
| if [ "$space" -ge 33 ]    | Checks if disk usage is ≥ 33%.                | Triggers disk alert condition.          |
| echo                      | Prints output message.                        | Displays alert or status message.       |
| mail -s                   | Sends an email with a subject.                | Sends disk usage alert.                 |
| else                      | Executes when condition fails.                | Handles normal disk usage case.         |
| fi                        | Ends the if-else block.                       | Marks completion of logic.              |


## 🖥️ Sample Output

<img width="1177" height="315" alt="diskalert" src="https://github.com/user-attachments/assets/50ff1afc-c27b-42e6-87c4-47e23d5eb96a" />
<img width="1132" height="487" alt="mailoutput" src="https://github.com/user-attachments/assets/0242d20c-b73d-4c55-b46c-d94e31c989e5" />

---

## 📜 Bash Script

```bash
#!/bin/bash

###################################################
#This is script to check space and send mail
#if disk usage exceeds the defined threshold
###################################################

space=$(df -h /mnt/app-data | grep -v "Filesystem" | awk '{print $5}' | tr -d '%')

if [ "$space" -ge 33 ]; then
    echo "Filesystem usage is High: $space%" | mail -s "Disk Alert: /mnt/app-data" deveshpatil562@gmail.com
else
    echo "Filesystem usage is fine"
fi



