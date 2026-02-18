# Bash Scripting Challenge – Log Analyzer & Report Generator  

👨‍💻 DevOps Journey  
🔗 LinkedIn: www.linkedin.com/in/devesh-patil-331958381  

---

# 📘 Introduction  

In this challenge, I built a **Log Analyzer Script** that automates:

- Log validation  
- Error counting  
- Critical event detection  
- Top 5 error message analysis  
- Daily summary report generation  
- Optional archiving of processed logs  

This simulates a real-world system administrator task.

---

# 📂 Log Analyzer Script  

## 📌 Script: log_analyzer.sh  

[#!/bin/bash  
set -euo pipefail  

LOG_FILE="${1:-}"  

if [ -z "$LOG_FILE" ]; then  
  echo "Error: Please provide a log file path."  
  exit 1  
fi  

if [ ! -f "$LOG_FILE" ]; then  
  echo "Error: File does not exist."  
  exit 1  
fi  

DATE=$(date +%Y-%m-%d)  
REPORT="log_report_$DATE.txt"  
TOTAL_LINES=$(wc -l < "$LOG_FILE")  

ERROR_COUNT=$(grep -Eci "ERROR|Failed" "$LOG_FILE" || true)  

CRITICAL_EVENTS=$(grep -n "CRITICAL" "$LOG_FILE" || true)  

TOP_ERRORS=$(grep "ERROR" "$LOG_FILE" |  
awk '{$1=$2=$3=""; print}' |  
sort | uniq -c | sort -rn | head -5 || true)  

echo "Total Errors: $ERROR_COUNT"  

echo "Generating report..."  

{  
echo "===== Log Analysis Report ====="  
echo "Date: $DATE"  
echo "Log File: $LOG_FILE"  
echo "Total Lines Processed: $TOTAL_LINES"  
echo "Total Error Count: $ERROR_COUNT"  
echo  

echo "--- Top 5 Error Messages ---"  
echo "$TOP_ERRORS"  
echo  

echo "--- Critical Events ---"  
echo "$CRITICAL_EVENTS"  
} > "$REPORT"  

echo "Report generated: $REPORT"  

# Optional Archiving  
ARCHIVE_DIR="archive"  
mkdir -p "$ARCHIVE_DIR"  
mv "$LOG_FILE" "$ARCHIVE_DIR/"  

echo "Log file moved to archive/"]

---

# 🖥 Console Output Example  

Running:  

[./log_analyzer.sh sample_log.log]

### ▶ Output:
- Total Errors: 129  
- Report generated: log_report_2026-02-18.txt  
- Log file moved to archive/  

---

# 📄 Sample Report Output (log_report_YYYY-MM-DD.txt)  

===== Log Analysis Report =====  

Date: 2026-02-18  
Log File: sample_log.log  
Total Lines Processed: 2048  
Total Error Count: 129  

--- Top 5 Error Messages ---  
45 Connection timed out  
32 File not found  
28 Permission denied  
15 Disk I/O error  
9 Out of memory  

--- Critical Events ---  
Line 84: 2025-07-29 10:15:23 CRITICAL Disk space below threshold  
Line 217: 2025-07-29 14:32:01 CRITICAL Database connection lost  

---

# 🔍 Commands & Tools Used  

- grep → Pattern searching  
- awk → Text processing  
- sort → Sorting output  
- uniq -c → Counting duplicates  
- wc -l → Line counting  
- date → Timestamp generation  
- mv → File movement  
- mkdir -p → Directory creation  

---

# 🧠 Key Learnings  

1. Log analysis can be fully automated using basic Linux tools.  
2. Combining grep, awk, sort, and uniq enables powerful text processing.  
3. Structured reporting improves monitoring and incident visibility.  

---

# 📂 Version Control Submission  

[mkdir -p 2026/day-20]  
[cp log_analyzer.sh day-20-solution.md 2026/day-20/]  
[git add .]  
[git commit -m "Log Analyzer & Report Generator"]  
[git push origin main]  

---

🚀 Automating log analysis is a real-world DevOps superpower.
