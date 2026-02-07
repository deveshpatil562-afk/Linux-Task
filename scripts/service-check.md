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

#!/bin/bash
# ==============================================================
# Script Name : service_check.sh
# Purpose     : Check if a Linux service is running.
#               If not running, automatically start the service.
# Author      : Devesh Patil
# ==============================================================


# Ask the user to enter the service name (example: nginx, ssh, docker)
read -p "Enter the name of service: " service


# Check the current status of the service using systemctl
# Possible outputs: active, inactive, failed, unknown
status=$(systemctl is-active $service)


# If the service status is "active"
if [ "$status" = "active" ]; then
        # Print message if service is already running
        echo "✅ Service is already running and active!"

else
        # If service is NOT running
        echo "❌ Service is not running. Starting the service now..."

        # Start the service
        systemctl start "$service"

        # Check and display the updated service status
        # systemctl status gives detailed info
        # grep "Active:" filters only the active status line
        new_status=$(systemctl status "$service" | grep "Active:")

        # Display confirmation message
        echo "🚀 Service has been started successfully!"
        echo "$new_status"
fi
