---
title: "Getting Started with Docker and Jenkins 🐳🛠"
datePublished: Tue Oct 31 2023 10:19:13 GMT+0000 (Coordinated Universal Time)
cuid: cloe6fkyr001q09lh4w1g1wzb
slug: getting-started-with-docker-and-jenkins
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698747471068/d0f418cb-36e9-4c96-9de1-25f6c10b7e29.png
tags: docker, devops, jenkins

---

---

**Docker** and **Jenkins** are two essential tools for DevOps and continuous integration. Docker allows you to containerize applications, making them portable and easy to manage, while Jenkins helps automate the building and deployment of software. In this guide, we'll walk you through the installation process for both Docker and Jenkins on your system.

## **Step 1: Installing Docker 🐋**

**For Linux:**

1. **Update Your System**: Open a terminal and update your package manager. 🔄
    
    ```bash
    sudo apt update
    ```
    
2. **Install Docker**: Install Docker using the package manager specific to your Linux distribution. For example, on Ubuntu, you can use `apt`. 📦
    
    ```bash
    sudo apt install docker.io
    ```
    
3. **Start and Enable Docker**: Start the Docker service and enable it to start at boot. 🚀
    
    ```bash
    sudo systemctl start docker
    sudo systemctl enable docker
    ```
    

### **Step 2: Installing Jenkins ☕**

1. **Download Jenkins**: Visit the [Jenkins website](https://www.jenkins.io/download/) and download the Jenkins WAR (Web Application Archive) file. You can also use the `wget` command to download it directly in your terminal. 🌐
    
    ```bash
    wget http://mirrors.jenkins.io/war/latest/jenkins.war
    ```
    
2. **Run Jenkins**: To start Jenkins, simply run the downloaded WAR file using Java. ☕
    
    ```bash
    java -jar jenkins.war
    ```
    
    Jenkins will start and be available at [`http://localhost:8080`](https://www.jenkins.io/download/) in your web browser. 🌐
    
3. **Unlock Jenkins**: To set up Jenkins, you need to retrieve the initial admin password. This password can be found in the terminal where you started Jenkins. 🔐
    
4. **Install Plugins**: Customize your Jenkins installation by selecting the plugins you need. 🧩
    
5. **Create an Admin User**: Set up an admin user and complete the Jenkins installation wizard. 👤
    

## **Step 3: Using Docker with Jenkins 🚢**

Once Jenkins is installed, you can integrate it with Docker to build and deploy applications in containers. To do this, you can install and configure plugins like "Docker" and "Docker Pipeline" within Jenkins. These plugins enable you to use Docker commands and build Docker images in your Jenkins pipelines. 🌐

### **Conclusion 🚀**

You've now successfully installed Docker and Jenkins on your system. With Docker, you can containerize applications, making them portable and easy to manage, while Jenkins helps automate your development and deployment processes. These tools are essential for modern software development and DevOps practices. Explore their capabilities, and start building and deploying your projects more efficiently. 🏗

Happy coding and automating! 🚀

**#Docker #Jenkins #DevOps #Containerization #CI/CD**