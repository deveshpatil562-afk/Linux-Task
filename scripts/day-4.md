# Shell Scripting Project – Log Rotation, Backup & Scheduled Maintenance  

👨‍💻 DevOps Journey  
🔗 LinkedIn: www.linkedin.com/in/devesh-patil-331958381  

---

# 📘 Introduction  

In this mini project, I applied shell scripting concepts to real-world scenarios:

- Log rotation automation  
- Server backup automation  
- Cron scheduling  
- Combined maintenance script  

All scripts, outputs, and cron entries are documented below.

---

# 📁 Log Rotation Script  

## 📌 Script: log_rotate.sh  

[#!/bin/bash  
set -euo pipefail  

LOG_DIR="${1:-}"  

if [ -z "$LOG_DIR" ] || [ ! -d "$LOG_DIR" ]; then  
  echo "Error: Directory does not exist."  
  exit 1  
fi  

compressed_count=$(find "$LOG_DIR" -name "*.log" -mtime +7 -type f | wc -l)  
deleted_count=$(find "$LOG_DIR" -name "*.gz" -mtime +30 -type f | wc -l)  

find "$LOG_DIR" -name "*.log" -mtime +7 -type f -exec gzip {} \;  
find "$LOG_DIR" -name "*.gz" -mtime +30 -type f -delete  

echo "Compressed files: $compressed_count"  
echo "Deleted old archives: $deleted_count"]

### ▶ Sample Output:
- Compressed files: 5  
- Deleted old archives: 2  

---

# 💾 Server Backup Script  

## 📌 Script: backup.sh  

[#!/bin/bash  
set -euo pipefail  

SOURCE="${1:-}"  
DEST="${2:-}"  

if [ -z "$SOURCE" ] || [ ! -d "$SOURCE" ]; then  
  echo "Error: Source directory does not exist."  
  exit 1  
fi  

mkdir -p "$DEST"  

TIMESTAMP=$(date +%Y-%m-%d)  
ARCHIVE="$DEST/backup-$TIMESTAMP.tar.gz"  

tar -czf "$ARCHIVE" "$SOURCE"  

if [ -f "$ARCHIVE" ]; then  
  echo "Backup created: $ARCHIVE"  
  du -h "$ARCHIVE"  
else  
  echo "Backup failed!"  
  exit 1  
fi  

find "$DEST" -name "backup-*.tar.gz" -mtime +14 -type f -delete]

### ▶ Sample Output:
- Backup created: /backup/backup-2026-02-18.tar.gz  
- 45M  /backup/backup-2026-02-18.tar.gz  

---

# ⏰ Crontab Configuration  

## 📌 View Existing Cron Jobs  

[crontab -l]

---

## 📖 Cron Syntax  

* * * * *  command  
│ │ │ │ │  
│ │ │ │ └── Day of week (0-7)  
│ │ │ └──── Month (1-12)  
│ │ └────── Day of month (1-31)  
│ └──────── Hour (0-23)  
└────────── Minute (0-59)  

---

## 📌 Cron Entries  

Run log rotation every day at 2 AM:

[0 2 * * * /path/to/log_rotate.sh /var/log/myapp]

Run backup every Sunday at 3 AM:

[0 3 * * 0 /path/to/backup.sh /source /backup]

Run health check script every 5 minutes:

[*/5 * * * * /path/to/health_check.sh]

---

# 🛠 Combined Scheduled Maintenance Script  

## 📌 Script: maintenance.sh  

[#!/bin/bash  
set -euo pipefail  

LOG_FILE="/var/log/maintenance.log"  

log_message() {  
  echo "$(date '+%Y-%m-%d %H:%M:%S') : $1" >> "$LOG_FILE"  
}  

run_log_rotation() {  
  /path/to/log_rotate.sh /var/log/myapp >> "$LOG_FILE" 2>&1  
}  

run_backup() {  
  /path/to/backup.sh /source /backup >> "$LOG_FILE" 2>&1  
}  

main() {  
  log_message "Maintenance started"  
  run_log_rotation  
  run_backup  
  log_message "Maintenance completed"  
}  

main]

---

## 📌 Cron Entry for Maintenance Script  

Run daily at 1 AM:

[0 1 * * * /path/to/maintenance.sh]

---

# 🧠 Key Learnings  

1. Automation reduces manual server maintenance effort.  
2. Combining strict mode with validation makes scripts reliable and production-safe.  
3. Cron enables fully automated infrastructure operations.  

---

# 📂 Version Control Submission  

[mkdir -p 2026/day-19]  
[cp *.sh 2026/day-19/]  
[git add .]  
[git commit -m "Shell Project – Log Rotation, Backup & Maintenance"]  
[git push origin main]  

---

🚀 Practical automation is the foundation of real-world DevOps.
