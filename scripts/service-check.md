# 🛠️ Linux Service Status Checker & Auto-Starter (Bash Script)

This Bash script helps you **check whether a Linux service is running** and **automatically starts it if it’s not**.  
It’s simple, practical, and perfect for **Linux beginners / freshers** who want hands-on scripting experience.

---

## 📌 What This Script Does

- Asks the user for a **service name**
- Checks the **current status** of the service
- If the service is:
  - ✅ **Running** → informs the user
  - ❌ **Not running** → starts the service automatically
- Confirms that the service has been started successfully

---

## 🧠 Why This Script Is Useful

- Avoids manual service checks
- Saves time for system administrators
- Helps beginners understand:
  - `systemctl`
  - condition checks
  - user input in Bash
- Can be used in **real-world Linux servers**

---

## 🖥️ Prerequisites

Before running this script, make sure:

- You are using a **Linux system with systemd**
- You have **sudo/root access**
- The service you want to check exists

Examples of services:
- `nginx`
- `apache2`
- `mysql`
- `ssh`
- `docker`

---

## 📜 The Script

```bash
#!/bin/bash

####################################################################
# This script checks if a service is running.
# If the service is not running, it starts the service automatically.
####################################################################

read -p "Enter the name of service: " service

status=$(systemctl is-active $service)

if [ $status = active ]; then
        echo "Service is in active state!!"
else
        echo "Service is not running. Let me start the service..."
        systemctl start "$service"
        new_status=$(systemctl status $service | grep "Active:")
        echo "Service has been started successfully :)"
fi

---

## 📋 Command Explanation Table

| Command / Syntax | Description | Why It Is Used |
|------------------|------------|----------------|
| `#!/bin/bash` | Tells the system to execute the script using the Bash shell. | Ensures the script runs correctly in a Bash environment. |
| `read -p` | Reads input from the user and displays a prompt message. | Allows the user to enter the service name dynamically. |
| `systemctl` | A systemd command used to manage Linux services. | Used to check, start, stop, and manage system services. |
| `systemctl is-active <service>` | Checks whether a service is currently running. | Helps determine if the service needs to be started. |
| `status=$(...)` | Stores the output of a command into a variable. | Allows reuse of command output in conditions. |
| `if [ condition ]` | Executes commands only if the condition is true. | Used for decision-making in the script. |
| `[ "$status" = "active" ]` | Compares the service status with the word `active`. | Confirms whether the service is running. |
| `echo` | Prints text to the terminal. | Displays user-friendly messages and status updates. |
| `else` | Executes when the `if` condition is false. | Handles the case when the service is not running. |
| `systemctl start <service>` | Starts the specified Linux service. | Automatically brings the service up if it is stopped. |
| `systemctl status <service>` | Displays detailed information about a service. | Used to verify the service start operation. |
| `grep "Active:"` | Filters output and displays lines containing `Active:`. | Shows only the important service status line. |
| `new_status=$(...)` | Stores filtered command output into a variable. | Helps display the updated service state. |
| `fi` | Ends the `if-else` conditional block. | Marks completion of the decision logic. |


