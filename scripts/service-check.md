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
