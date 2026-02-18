# Shell Scripting – Loops, Arguments & Error Handling  

👨‍💻 DevOps Journey  
🔗 LinkedIn: www.linkedin.com/in/devesh-patil-331958381  

---

# 📘 Introduction  

In this module, I leveled up my shell scripting skills by working with:

- For loops  
- While loops  
- Command-line arguments  
- Package installation via script  
- Error handling & root checks  

All scripts are documented below with outputs and learnings.

---

# 🔁 For Loop Implementation  

## 📌 Script: for_loop.sh  

Loops through a list of 5 fruits and prints each one.

[#!/bin/bash  
for fruit in Apple Banana Mango Orange Grapes  
do  
  echo "Fruit: $fruit"  
done]

### ▶ Output:
- Fruit: Apple  
- Fruit: Banana  
- Fruit: Mango  
- Fruit: Orange  
- Fruit: Grapes  

---

## 📌 Script: count.sh  

Prints numbers from 1 to 10 using a for loop.

[#!/bin/bash  
for i in {1..10}  
do  
  echo $i  
done]

### ▶ Output:
- 1  
- 2  
- 3  
- 4  
- 5  
- 6  
- 7  
- 8  
- 9  
- 10  

---

# 🔄 While Loop Implementation  

## 📌 Script: countdown.sh  

Takes a number from the user and counts down to 0.

[#!/bin/bash  
echo "Enter a number:"  
read num  

while [ $num -ge 0 ]  
do  
  echo $num  
  num=$((num-1))  
done  

echo "Done!"]

### ▶ Output Example (Input: 5):
- 5  
- 4  
- 3  
- 2  
- 1  
- 0  
- Done!  

---

# 🎯 Command-Line Arguments  

## 📌 Script: greet.sh  

Accepts a name as argument and prints greeting.

[#!/bin/bash  

if [ -z "$1" ]  
then  
  echo "Usage: ./greet.sh <name>"  
else  
  echo "Hello, $1!"  
fi]

### ▶ Output:
- Hello, Devesh!  
OR  
- Usage: ./greet.sh <name>  

---

## 📌 Script: args_demo.sh  

Demonstrates special argument variables.

[#!/bin/bash  

echo "Script Name: $0"  
echo "Total Arguments: $#"  
echo "All Arguments: $@"]

### ▶ Output Example:
Command: ./args_demo.sh DevOps Linux Git  

- Script Name: ./args_demo.sh  
- Total Arguments: 3  
- All Arguments: DevOps Linux Git  

---

# 📦 Package Installation via Script  

## 📌 Script: install_packages.sh  

Checks if packages are installed and installs if missing.  
Includes root validation.

[#!/bin/bash  

if [ "$EUID" -ne 0 ]; then  
  echo "Run as root"  
  exit 1  
fi  

packages="nginx curl wget"  

for pkg in $packages  
do  
  if dpkg -s $pkg &> /dev/null || rpm -q $pkg &> /dev/null  
  then  
    echo "$pkg is already installed"  
  else  
    echo "Installing $pkg..."  
    apt install -y $pkg || yum install -y $pkg  
  fi  
done]

### ▶ Output:
- nginx is already installed  
- Installing curl...  
- wget is already installed  

Run as root:  
[sudo -i]  
OR  
[sudo su]  

---

# 🛡 Error Handling in Scripts  

## 📌 Script: safe_script.sh  

Implements strict mode and safe execution.

[#!/bin/bash  

set -e  

mkdir /tmp/devops-test || echo "Directory already exists"  

cd /tmp/devops-test || { echo "Failed to enter directory"; exit 1; }  

touch test_file.txt  

echo "File created successfully"]

### ▶ Output:
- Directory already exists (if present)  
- File created successfully  

---

# 🧠 Key Learnings  

1. Loops help automate repetitive tasks efficiently.  
2. Command-line arguments make scripts dynamic and reusable.  
3. Error handling (set -e, ||, root validation) improves script reliability and safety.  

---

# 📂 Version Control Submission  

[mkdir -p 2026/day-17]  
[cp *.sh 2026/day-17/]  
[git add .]  
[git commit -m "Scripting – Loops, Arguments & Error Handling"]  
[git push origin main]  

---

🚀 Consistency builds mastery in DevOps.
