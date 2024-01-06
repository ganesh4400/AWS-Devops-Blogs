---
title: "Day 5 : Advanced Linux Shell Scripting for DevOps Engineers with User Management"
datePublished: Fri Oct 27 2023 09:47:27 GMT+0000 (Coordinated Universal Time)
cuid: clo8fjbfh000108idcui63dso
slug: day-5-advanced-linux-shell-scripting-for-devops-engineers-with-user-management
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698393090677/ddffba77-2b4c-4618-8304-929c78091c86.png
tags: linux, devops, shell-script

---

## **Introduction**

Welcome to Day 5 of your DevOps journey! In today's task, we will delve into advanced Linux shell scripting, covering topics such as dynamic directory creation, script backups, and user management. Let's get started!

### **Task 1: Dynamic Directory Creation with Shell Script**

First, let's create a Bash script named `create_directories.sh` to dynamically create directories based on user input.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698398336879/338fe058-97ba-4ebb-a12f-ea156a581d61.png align="center")

This script takes three arguments: the directory name, the start number, and the end number. It creates directories in the specified range within the given directory name.

### **Task 2: Script Backup**

Backing up your scripts and work is crucial. You can create a simple backup script like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698398569174/a2d83169-8bd5-4498-a108-cf2c9c27c218.png align="center")

This script creates a backup directory with the current date and copies all your scripts into it. This way, you can easily retrieve your work if something goes wrong.

### **Task 3: Automating Backups with Cron**

Cron is a powerful task scheduler in Linux. You can use it to automate the backup script. Open your crontab for editing using `crontab -e` and add the following line to run the backup script daily at midnight:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698399224668/6fac987c-a8d8-471b-b73f-02cdf4b53728.png align="center")

Replace `/path/to/backup_script.sh` with the actual path to your backup script.

### **Task 4: User Management in Linux**

User management in Linux is vital for system administration. Here are some essential commands:

* `useradd`: Create a new user.
    
* `passwd`: Set or change the user's password.
    
* `userdel`: Delete a user.
    
* `usermod`: Modify user properties.
    
* `groupadd`: Create a new group.
    
* `useradd -G`: Add a user to a group.
    

To create a new user, for example, use:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698399324835/d4abee7c-52ac-410b-971c-5131b56ff329.png align="center")

To add a user to group, use:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698399916830/78a04c39-70e7-445f-abd2-b8a9664ecbe3.png align="center")

Replace `groupname` and `username` accordingly.

These are just a few basics of user management. As a DevOps engineer, you'll often need to create, manage, and configure users and groups for different purposes.

## **Conclusion**

Day 5 of your DevOps journey has introduced you to advanced Linux shell scripting, script backups, and user management. These skills are essential for system administration and automating tasks. Keep exploring and practicing to become a proficient DevOps engineer. Stay tuned for more exciting challenges in your DevOps adventure! 🚀

#DevOps

#Linux

#ShellScripting

#UserManagement

#CronJobs