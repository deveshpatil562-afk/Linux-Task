# Shell Scripting Cheat Sheet – Personal DevOps Reference Guide  

👨‍💻 DevOps Journey  
🔗 LinkedIn: www.linkedin.com/in/devesh-patil-331958381  

---

# ⚡ Quick Reference Table  

| Topic | Key Syntax | Example |
|-------|------------|---------|
| Variable | VAR="value" | NAME="DevOps" |
| Argument | $1, $2 | ./script.sh arg1 |
| If | if [ condition ]; then | if [ -f file ]; then |
| For loop | for i in list; do | for i in 1 2 3; do |
| Function | name() { ... } | greet() { echo "Hi"; } |
| Grep | grep pattern file | grep -i "error" log.txt |
| Awk | awk '{print $1}' file | awk -F: '{print $1}' /etc/passwd |
| Sed | sed 's/old/new/g' file | sed -i 's/foo/bar/g' config.txt |

---

# 🧱 Basics  

## Shebang  
[#!/bin/bash] → Tells system to use Bash interpreter.

## Run a Script  
[chmod +x script.sh]  
[./script.sh]  
[bash script.sh]

## Comments  
[# This is a comment]  
[echo "Hello" # Inline comment]

## Variables  
[NAME="DevOps"]  
[echo $NAME]  
[echo "$NAME"]  
[echo '$NAME']

## Read User Input  
[read USERNAME]

## Command-Line Arguments  
[$0 → Script name]  
[$1 → First argument]  
[$# → Total arguments]  
[$@ → All arguments]  
[$? → Last exit status]

---

# 🔎 Operators & Conditionals  

## String Comparison  
[if [ "$a" = "$b" ]]  
[-z "$var"] → Empty  
[-n "$var"] → Not empty  

## Integer Comparison  
[-eq, -ne, -lt, -gt, -le, -ge]

## File Tests  
[-f file] → File exists  
[-d dir] → Directory exists  
[-e file] → Exists  
[-r file] → Readable  
[-w file] → Writable  
[-x file] → Executable  
[-s file] → Not empty  

## If-Else  
[if [ condition ]; then  
  command  
elif [ condition ]; then  
  command  
else  
  command  
fi]

## Logical Operators  
[command1 && command2]  
[command1 || command2]  
[! condition]

## Case Statement  
[case $var in  
  1) echo "One" ;;  
  2) echo "Two" ;;  
  *) echo "Other" ;;  
esac]

---

# 🔁 Loops  

## For Loop (List-Based)  
[for i in 1 2 3; do echo $i; done]

## For Loop (C-Style)  
[for ((i=1;i<=5;i++)); do echo $i; done]

## While Loop  
[while [ condition ]; do command; done]

## Until Loop  
[until [ condition ]; do command; done]

## Loop Control  
[break] → Exit loop  
[continue] → Skip iteration  

## Loop Over Files  
[for file in *.log; do echo $file; done]

## Loop Over Command Output  
[while read line; do echo $line; done < file.txt]

---

# 🧩 Functions  

## Define Function  
[greet() { echo "Hello"; }]

## Call Function  
[greet]

## Pass Arguments  
[greet "Devesh"] → Access via [$1]

## Return Values  
[return 1] → Exit code  
[echo "value"] → Output value  

## Local Variables  
[local VAR="value"]

---

# 🔍 Text Processing Commands  

## Grep  
[grep "error" file]  
[-i] Ignore case  
[-r] Recursive  
[-c] Count  
[-n] Line number  
[-v] Invert match  
[-E] Extended regex  

## Awk  
[awk '{print $1}' file]  
[-F:] → Field separator  
[BEGIN {print "Start"}]  

## Sed  
[sed 's/old/new/g' file]  
[sed -i 's/foo/bar/g' file]  
[sed '2d' file] → Delete line 2  

## Cut  
[cut -d: -f1 file]

## Sort  
[sort file]  
[sort -n] → Numeric  
[sort -r] → Reverse  
[sort -u] → Unique  

## Uniq  
[uniq file]  
[uniq -c] → Count  

## Tr  
[tr 'a-z' 'A-Z']  
[tr -d '\n']

## Wc  
[wc -l file] → Lines  
[wc -w file] → Words  
[wc -c file] → Characters  

## Head / Tail  
[head -5 file]  
[tail -5 file]  
[tail -f file] → Follow  

---

# 🚀 Useful One-Liners  

Find and delete files older than 7 days:  
[find /path -type f -mtime +7 -delete]

Count lines in all .log files:  
[wc -l *.log]

Replace string across multiple files:  
[sed -i 's/old/new/g' *.conf]

Check if service is running:  
[systemctl is-active nginx]

Monitor disk usage alert:  
[df -h | awk '$5 > 80 {print $0}']

Tail log and filter errors live:  
[tail -f app.log | grep "ERROR"]

---

# 🛡 Error Handling & Debugging  

## Exit Codes  
[$?] → Last command status  
[exit 0] → Success  
[exit 1] → Failure  

## Strict Mode  
[set -e] → Exit on error  
[set -u] → Error on unset variable  
[set -o pipefail] → Catch pipe errors  
[set -x] → Debug trace  

## Trap  
[trap 'echo Cleanup done' EXIT]

---

# 🧠 Key Takeaways  

1. Shell scripting becomes powerful when combined with text-processing tools.  
2. Strict mode prevents silent failures in production scripts.  
3. Real-world DevOps tasks rely heavily on automation and one-liners.  

---

✅ This cheat sheet serves as a practical, job-ready reference guide for everyday DevOps scripting tasks.
