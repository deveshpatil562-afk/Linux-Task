# Shell Scripting – Functions, Strict Mode & Real-World Patterns  

👨‍💻 DevOps Journey  
🔗 LinkedIn: www.linkedin.com/in/devesh-patil-331958381  

---

# 📘 Introduction  

In this module, I focused on writing cleaner, reusable, and production-ready scripts using:

- Functions  
- Strict mode (set -euo pipefail)  
- Return values and local variables  
- A structured real-world system reporting script  

All scripts with outputs and explanations are documented below.

---

# 🔧 Basic Functions  

## 📌 Script: functions.sh  

[#!/bin/bash  

greet() {  
  echo "Hello, $1!"  
}  

add() {  
  sum=$(($1 + $2))  
  echo "Sum: $sum"  
}  

greet "Devesh"  
add 10 20]

### ▶ Output:
- Hello, Devesh!  
- Sum: 30  

---

# 🔁 Functions with System Checks  

## 📌 Script: disk_check.sh  

[#!/bin/bash  

check_disk() {  
  echo "Disk Usage:"  
  df -h /  
}  

check_memory() {  
  echo "Memory Usage:"  
  free -h  
}  

main() {  
  check_disk  
  echo "----------------------"  
  check_memory  
}  

main]

### ▶ Output:
- Disk usage details of `/`  
- Memory usage summary (total, used, free)  

---

# 🛡 Strict Mode – set -euo pipefail  

## 📌 Script: strict_demo.sh  

[#!/bin/bash  
set -euo pipefail  

echo "Testing undefined variable:"  
echo $UNDEFINED_VAR  

echo "Testing failing command:"  
false  

echo "Testing pipe failure:"  
grep "text" nonexistentfile | sort]

### ▶ Output Behavior:

- Script exits immediately when using undefined variable (`set -u`)  
- Script exits when a command fails (`set -e`)  
- Script exits if any command in a pipeline fails (`set -o pipefail`)  

---

## 📖 Explanation of Strict Mode  

- **set -e →** Exit immediately if a command exits with non-zero status  
- **set -u →** Exit if an undefined variable is used  
- **set -o pipefail →** Return failure if any command inside a pipe fails  

Strict mode makes scripts safer and production-ready.

---

# 🔐 Local Variables in Functions  

## 📌 Script: local_demo.sh  

[#!/bin/bash  

test_local() {  
  local message="Inside Function"  
  echo $message  
}  

test_global() {  
  message="Global Variable"  
}  

test_local  
echo $message  

test_global  
echo $message]

### ▶ Output:
- Inside Function  
- (No output — local variable not accessible outside)  
- Global Variable  

### 🔎 Observation:
Local variables remain inside the function scope, while normal variables affect global scope.

---

# 🖥 Build Script – System Info Reporter  

## 📌 Script: system_info.sh  

[#!/bin/bash  
set -euo pipefail  

print_header() {  
  echo "============================="  
  echo "$1"  
  echo "============================="  
}  

hostname_info() {  
  hostname  
  uname -a  
}  

uptime_info() {  
  uptime  
}  

disk_usage() {  
  df -h | sort -rk5 | head -5  
}  

memory_usage() {  
  free -h  
}  

top_cpu_processes() {  
  ps -eo pid,comm,%cpu --sort=-%cpu | head -6  
}  

main() {  
  print_header "HOSTNAME & OS INFO"  
  hostname_info  

  print_header "UPTIME"  
  uptime_info  

  print_header "DISK USAGE (TOP 5)"  
  disk_usage  

  print_header "MEMORY USAGE"  
  memory_usage  

  print_header "TOP 5 CPU PROCESSES"  
  top_cpu_processes  
}  

main]

### ▶ Output:
- Hostname and OS details  
- System uptime  
- Top 5 disk usage entries  
- Memory usage summary  
- Top 5 CPU-consuming processes  

Clean, readable, and structured output.

---

# 🧠 Key Learnings  

1. Functions improve script reusability and structure.  
2. Strict mode (set -euo pipefail) prevents silent failures and unsafe execution.  
3. Local variables help maintain clean scope and avoid unexpected behavior.  

---

# 📂 Version Control Submission  

[mkdir -p 2026/day-18]  
[cp *.sh 2026/day-18/]  
[git add .]  
[git commit -m "Scripting – Functions & Strict Mode"]  
[git push origin main]  

---

🚀 Writing safer and production-ready shell scripts.
