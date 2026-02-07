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
==============================
 SAMPLE OUTPUT
==============================
Enter the name of service: postfix
Service is not running. Let me start the service...
Service has been started successfully :)
Active: active (running)

==============================
 BASH SCRIPT
==============================
#!/bin/bash
# Uses Bash shell to execute this script.

read -p "Enter the name of service: " service
# Takes service name input from the user.

status=$(systemctl is-active $service)
# Checks whether the service is active or not.

if [ "$status" = "active" ]; then
    echo "Service is in active state!!"
    # Prints message if service is already running.
else
    echo "Service is not running. Let me start the service..."
    # Prints message when service is stopped.

    systemctl start "$service"
    # Starts the specified Linux service.

    new_status=$(systemctl status "$service" | grep "Active:")
    # Fetches and filters the active status line.

    echo "Service has been started successfully :)"
    # Prints success message.

    echo "$new_status"
    # Displays updated service status.
fi
# Ends the if-else block.

==============================
 COMMAND EXPLANATION TABLE
==============================

| Command / Syntax | Description | Why It Is Used |
|------------------|-------------|----------------|
| #!/bin/bash | Specifies Bash as the script interpreter. | Ensures script runs using Bash shell. |
| read -p | Reads user input with a prompt message. | Accepts service name dynamically. |
| systemctl | systemd tool to manage Linux services. | Used to control service states. |
| systemctl is-active <service> | Checks if a service is running. | Determines whether restart is needed. |
| status=$(...) | Stores command output in a variable. | Enables condition checking. |
| if [ condition ] | Conditional execution block. | Adds decision-making logic. |
| [ "$status" = "active" ] | Compares service state with active. | Confirms running service. |
| echo | Prints output to terminal. | Displays messages to user. |
| else | Executes when if condition fails. | Handles stopped service case. |
| systemctl start <service> | Starts a Linux service. | Automatically recovers service. |
| systemctl status <service> | Shows detailed service info. | Verifies service startup. |
| grep "Active:" | Filters Active status line. | Improves output readability. |
| new_status=$(...) | Stores filtered status output. | Displays updated status. |
| fi | Ends conditional block. | Marks logic completion. |
