# 🛠️ Linux Service Status Checker & Auto Starter (Bash Script)

This project contains a **simple yet powerful Bash script** that checks whether a Linux service is running.  
If the service is **not running**, the script **automatically starts it**.

This project is designed especially for **freshers and Linux beginners** to understand real-world Bash scripting and Linux service management.

---

📌 WHAT THIS SCRIPT DOES


- Prompts the user to enter a **Linux service name**
- Checks whether the service is **running or not**
- If the service is:
  - ✅ **Active** → Displays a confirmation message
  - ❌ **Inactive** → Starts the service automatically
- Confirms that the service has been started

---

🎯 WHY THIS SCRIPT IS USEFUL


- Automates service checking
- Reduces manual work for administrators
- Helps freshers learn:
  - Bash scripting basics
  - Linux services
  - Conditional logic (if-else)
  - systemctl command usage
- Can be used as a **resume / GitHub project**

---

**🧠 PREREQUISITES**


Before running this script, make sure:

- You are using a **Linux system with systemd**
- You have **sudo/root access**
- The service exists on your system

Example services:
- postfix
- nginx
- ssh
- docker
- mysql

---

**📜 BASH SCRIPT**


## 📜 Bash Script

```bash
#!/bin/bash

# This is a script to check if any service is running or not.
# If the service is not running, it will start the service.

read -p "Enter the name of service: " service

status=$(systemctl is-active $service)

if [ $status = active ]; then
    echo "Service is in active state!!"
else
    echo "Service is not running Currently let me start the service"
    systemctl start "$service"
    new_status=$(systemctl status $service | grep "Active:")
    echo "Service has been started :))"
fi

---

**🔍 HOW THE SCRIPT WORKS (STEP-BY-STEP)**


1. Script starts using the **Bash shell**
2. User enters the **service name**
3. systemctl is-active checks the service status
4. Output is stored in a variable
5. if-else logic checks the service state
6. If stopped, the service is started automatically
7. Success message is displayed

---

**🖥️ SAMPLE OUTPUT**


Enter the name of service: postfix
Service is not running Currently let me start the service
Service has been started :))

---

**📋 COMMAND EXPLANATION TABLE (FOR FRESHERS)**


| Command / Syntax | Description | Why It Is Used |
|------------------|-------------|----------------|
| #!/bin/bash | Specifies Bash as the script interpreter. | Ensures the script runs using Bash. |
| read -p | Reads user input with a prompt message. | Accepts service name dynamically. |
| systemctl | Linux utility to manage services. | Controls service operations. |
| systemctl is-active <service> | Checks if a service is running. | Determines service status. |
| status=$(...) | Stores command output in a variable. | Used for conditional logic. |
| if [ condition ] | Executes code when condition is true. | Decision-making logic. |
| [ $status = active ] | Compares service status with active. | Confirms service is running. |
| echo | Prints output to terminal. | Displays messages to the user. |
| else | Executes when if condition fails. | Handles stopped service case. |
| systemctl start <service> | Starts the Linux service. | Automatically recovers service. |
| systemctl status <service> | Shows detailed service information. | Verifies service state. |
| grep "Active:" | Filters Active status line. | Cleaner and readable output. |
| fi | Ends the if-else block. | Marks completion of logic. |

