# 🐚 Shell Scripting Basics

![Bash](https://img.shields.io/badge/Shell-Bash-green)
![Level](https://img.shields.io/badge/Level-Beginner-blue)
![Focus](https://img.shields.io/badge/Focus-Scripting-orange)
![Practice](https://img.shields.io/badge/Hands--On-Yes-success)

---

## 📌 Overview

This module covers the **fundamentals of shell scripting** required for automation in DevOps and Linux environments.

### 🎯 Objectives

- Understand the importance of the **shebang (`#!/bin/bash`)**
- Work with **variables**, `echo`, and `read`
- Implement **if-else conditional logic**
- Perform **file checks**
- Automate a simple **service status check**

---

# 🧠 Task 1: Your First Script

## 📄 hello.sh

[#!/bin/bash
echo "Hello, DevOps!"
]

### ▶ Run the Script

[chmod +x hello.sh
./hello.sh
]

### 🖥 Output

[Hello, DevOps!
]

### 📘 Key Learning

- `#!/bin/bash` specifies the interpreter.
- Without shebang:
  - `bash hello.sh` works
  - `./hello.sh` may fail or use a different shell
- Always define the interpreter for predictable behavior.

---

# 🧠 Task 2: Working with Variables

## 📄 variables.sh

[#!/bin/bash

NAME="Shubham"
ROLE="DevOps Engineer"

echo "Hello, I am $NAME and I am a $ROLE"

echo 'Hello, I am $NAME and I am a $ROLE'
]

### 🖥 Output

[Double quotes → Variables expand:
Hello, I am Shubham and I am a DevOps Engineer

Single quotes → Variables remain literal:
Hello, I am $NAME and I am a $ROLE
]

### 📘 Key Learning

- No spaces around `=`
- Double quotes `" "` allow variable expansion
- Single quotes `' '` prevent expansion

---

# 🧠 Task 3: User Input with `read`

## 📄 greet.sh

[#!/bin/bash

read -p "Enter your name: " NAME
read -p "Enter your favourite tool: " TOOL

echo "Hello $NAME, your favourite tool is $TOOL"
]

### 🖥 Example Output

[Enter your name: Shubham
Enter your favourite tool: Docker
Hello Shubham, your favourite tool is Docker
]

### 📘 Key Learning

- `read -p` allows inline user prompts
- User input can be stored in variables
- Enables interactive scripts

---

# 🧠 Task 4: Conditional Statements

## 📄 check_number.sh

[#!/bin/bash

read -p "Enter a number: " NUM

if [ $NUM -gt 0 ]; then
    echo "The number is positive."
elif [ $NUM -lt 0 ]; then
    echo "The number is negative."
else
    echo "The number is zero."
fi
]

---

## 📄 file_check.sh

[#!/bin/bash

read -p "Enter filename: " FILE

if [ -f "$FILE" ]; then
    echo "File exists."
else
    echo "File does not exist."
fi
]

### 📘 Key Learning

- `if [ condition ]; then`
- `elif` for additional conditions
- `-f` checks if a file exists
- Always quote variables when working with filenames

---

# 🧠 Task 5: Combine Everything

## 📄 server_check.sh

[#!/bin/bash

SERVICE="nginx"

read -p "Do you want to check the status of $SERVICE? (y/n): " CHOICE

if [ "$CHOICE" == "y" ]; then
    systemctl status $SERVICE
    if systemctl is-active --quiet $SERVICE; then
        echo "$SERVICE is running."
    else
        echo "$SERVICE is not running."
    fi
elif [ "$CHOICE" == "n" ]; then
    echo "Skipped."
else
    echo "Invalid input."
fi
]

### 📘 Key Learning

- Nested `if` statements
- Service status check using `systemctl`
- Basic automation logic
- Real-world DevOps scripting foundation

---

# 🏁 Final Takeaways

✅ Always define the interpreter with shebang  
✅ Understand quoting rules for variable expansion  
✅ Use conditionals to automate decision-making  
✅ Combine logic + user input for practical automation  

---

# 🚀 Skills Practiced

- Bash fundamentals  
- Linux command execution  
- Interactive scripting  
- Conditional logic  
- Service monitoring basics  

---

> 📌 This repository demonstrates hands-on practice with foundational shell scripting concepts used in real-world DevOps environments.
