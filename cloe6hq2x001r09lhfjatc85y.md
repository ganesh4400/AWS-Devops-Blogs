---
title: "Day 7 : Understanding Package Managers, Systemctl, and Systemd in Linux 🚀"
datePublished: Tue Oct 31 2023 10:20:53 GMT+0000 (Coordinated Universal Time)
cuid: cloe6hq2x001r09lhfjatc85y
slug: day-7-understanding-package-managers-systemctl-and-systemd-in-linux
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698748173305/82dfc7d0-f104-498c-88b4-a599cdf615e4.png
tags: rpm, linux, debugging, package-manager

---

Welcome to Day 7 of your DevOps journey! Today, we're delving into essential aspects of Linux system administration. We'll explore package managers, `systemctl`, and `systemd`, which are key components of managing a Linux system. These skills are crucial for maintaining a healthy and efficient Linux system. Let's dive into the tasks for the day.

## **The Role of Package Managers 📦**

**Package managers** are like the digital librarians of your Linux system. They are responsible for the management, installation, updating, and removal of software packages. These software packages can include applications, libraries, and system utilities. Different Linux distributions come with their package management systems, each with its unique characteristics and commands.

## **Task 1: Package Managers**

Linux distributions often come with their package management systems. These package managers are vital for installing, updating, and removing software packages. Two of the most commonly used package managers are `apt` (used in Debian-based systems like Ubuntu) and `yum` (used in Red Hat-based systems like CentOS).

### **Debian-based Systems (**`apt`):

* **Install a package**: `sudo apt-get install package_name`
    
* **Update package information**: `sudo apt-get update`
    
* **Upgrade installed packages**: `sudo apt-get upgrade`
    
* **Remove a package**: `sudo apt-get remove package_name`
    

### **Red Hat-based Systems (**`yum`):

* **Install a package**: `sudo yum install package_name`
    
* **Update package information**: `sudo yum check-update`
    
* **Upgrade installed packages**: `sudo yum update`
    
* **Remove a package**: `sudo yum remove package_name`
    

## Tasks:

1. You have to install docker and Jenkins in your system from your terminal using package managers
    
2. Write a small blog or article to install these tools using package managers on Ubuntu and CentOS
    
    You can read my other blog to install docker and Jenkins on linux system at this link: [https://ganeshshinde4.hashnode.dev/getting-started-with-docker-and-jenkins](https://ganeshshinde4.hashnode.dev/getting-started-with-docker-and-jenkins)
    

## **Task 2: Systemctl and Systemd ⚙️**

`systemctl` is a powerful command for controlling services in a Linux system, and it is closely related to `systemd`.

**Systemd** is an init system and service manager for Linux, which replaces the traditional `init` system. It manages system startup and various system processes, allowing for faster boot times and efficient system management.

### **Basic** `systemctl` Commands:

* **Start a service**: `sudo systemctl start service_name`
    
* **Stop a service**: `sudo systemctl stop service_name`
    
* **Enable a service to start at boot**: `sudo systemctl enable service_name`
    
* **Disable a service from starting at boot**: `sudo systemctl disable service_name`
    
* **Check the status of a service**: `sudo systemctl status service_name`
    

## Tasks:

1. Check the status of the docker service in your system (make sure you completed the above tasks, else docker won't be installed)
    
2. stop the service Jenkins and post before and after screenshots
    

## **Conclusion**

Understanding package managers, `systemctl`, and `systemd` is foundational for any DevOps engineer or Linux system administrator. Efficiently managing software installations, maintaining services, and system initialization are key responsibilities in ensuring a smoothly running system. Keep exploring, practicing, and learning as you continue your DevOps journey.

Happy managing, and stay curious! 🚀

**#DevOps #Linux #PackageManagement #Systemctl #Systemd #ServiceManagement #SysAdmin #LearningAndGrowing**