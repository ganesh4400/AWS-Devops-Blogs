---
title: ""Mastering Two-Tier Flask App Deployment with Docker: A Step-by-Step Guide for deployment""
datePublished: Sat Jan 20 2024 09:57:05 GMT+0000 (Coordinated Universal Time)
cuid: clrlwb4hs000d09l4h6w788hn
slug: mastering-two-tier-flask-app-deployment-with-docker-a-step-by-step-guide-for-deployment
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705740462179/3bf11a82-558b-497f-a17f-bc2df87037da.png
tags: docker, aws, projects, devops

---

🚀 **Setting Up a Two-Tier Flask App on Docker** 🚀

Before we dive into the exciting journey of setting up a two-tier Flask app using Docker, let's make sure you have everything you need. Follow these preliminary steps to ensure a smooth setup:

**Prerequisites:**

1. **Basic Knowledge of Docker:** Before we begin, make sure you have a basic understanding of Docker concepts. If you're new to Docker, consider going through the official documentation.
    
2. **Docker Installed:** Ensure Docker is installed on your machine. If not, you can follow the installation instructions on the official Docker website.
    
3. **Git Installed:** We'll be cloning a GitHub repository, so ensure Git is installed. If not, you can download and install Git from [git.com](https://git-scm.com/).
    
4. **Docker Hub Account:** To push your custom Flask app image, you'll need a Docker Hub account. If you don't have one, sign up at [hub.docker.com](https://git-scm.com/).
    

Now that we have the prerequisites covered, let's dive into the detailed steps of setting up our two-tier Flask app with Docker. Buckle up and let's get started!

👉 **Note:** If you already have the prerequisites in place, feel free to skip ahead to the main steps in the next section.

1. 🔧 **Install Docker:**
    
    ```bash
    sudo apt update
    sudo apt install docker.io
    ```
    
    This ensures that your system is updated and Docker is installed.
    
2. 🐳 **Check Docker Processes:**
    
    ```bash
    docker ps
    ```
    
    Verify that Docker is running and displaying any active containers.
    
3. 🌀 **Clone the Two-Tier Flask App Repository:**
    
    ```bash
    git clone https://github.com/ganesh4400/two-tier-flask-app.git
    cd two-tier-flask-app/
    ```
    
    Clone the Flask app repository and navigate to the project directory.
    
4. ✏️ **Edit Dockerfile:**
    
    ```bash
    FROM python:3.9-slim
    
    WORKDIR /app
    
    RUN apt-get update -y \
            && apt-get upgrade -y \
            && apt-get install -y gcc default-libmysqlclient-dev pkg-config \
            && rm -rf /var/lib/apt/lists/*
    
    COPY requirements.txt .
    
    RUN pip install mysqlclient
    RUN pip install -r requirements.txt
    
    COPY . .
    
    CMD ["python","app.py"]
    ```
    
    Create a Dockerfile to build the image for your Flask app, ensuring the necessary dependencies are installed.
    
5. 🏗️ **Build Docker Image:**
    
    ```bash
    docker build . -t flaskapp
    ```
    
    Build a Docker image for your Flask app based on the Dockerfile.
    
6. 🖼️ **List Docker Images:**
    
    ```bash
    docker images
    ```
    
    View the list of Docker images to ensure your 'flaskapp' image is successfully created.
    
7. 🌐 **Create Docker Network & Inspect Network:**
    
    ```bash
    docker network create twotier
    docker network ls
    docker network inspect twotier
    ```
    
    Create a Docker network for communication between containers.
    
8. 🚢 **Run MySQL Container:**
    
    ```bash
    docker run -d -p 3306:3306 --network=twotier -e MYSQL_DATABASE=myDb -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin -e MYSQL_ROOT_PASSWORD=admin --name=mysql mysql:5.7
    ```
    
    Start a MySQL container with specified environment variables.
    
9. 🚀 **Run Flask App Container:**
    
    ```bash
    docker run -d -p 5000:5000 --network=twotier -e MYSQL_HOST=mysql -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin -e MYSQL_DB=myDb --name=flaskapp flaskapp:latest
    ```
    
    Launch the Flask app container with connections to the MySQL container.
    
10. 🚦 **Check Running Containers & Network between containers:**
    
    ```bash
    docker ps
    docker network inspect twotier
    ```
    
    Ensure both containers are running and connected in the 'twotier' network.
    
11. 🔑 **Login to Docker Hub:**
    
    ```bash
    docker login
    # Enter your ID & Password
    ```
    
    Log in to Docker Hub to push your custom Flask app image.
    
12. 🏷️ **Tag and Push Flask App Image to DockerHub:**
    
    ```bash
    docker tag flaskapp:latest dockerhubid/flaskapp:latest
    docker images
    docker push dockerhubid/flaskapp:latest
    ```
    
    Tag your image and push it to your Docker Hub repository.
    
13. 🛠️ **Access Container Shell :**
    
    ```bash
    docker exec -it <container_id> bash
    ```
    
    Access the shell of your container. We use this to access our database container to do below configurations.
    
14. **Set Up Database and Table:**
    
    ```bash
    mysql -u root -p
    # Enter your Password
    use myDb;     # Select database
    CREATE TABLE messages (
        id INT AUTO_INCREMENT PRIMARY KEY,
        message TEXT
    );
    #create tables in database
    ```
    
    You can verify app is running by hitting below url in the browser
    
    **URL:** server\_ip:5000
    
15. 📝 **Install Docker Compose and Edit Docker Compose Configuration:**
    
    ```bash
    apt install docker-compose
    vi docker-compose.yml
    ```
    
    If you don't want to run two separate commands to run each containers we can use docker-compose to run both. Use a text editor to create or modify the Docker Compose configuration file.
    
16. 📝 **Edit Docker Compose Configuration:**
    
    ```bash
    version: '3'
    services:
      backend:
        image: dockerhubid/flaskapp:latest
        ports:
          - "5000:5000"
        environment:
           MYSQL_HOST: "mysql"
           MYSQL_USER: "admin"
           MYSQL_PASSWORD: "admin"
           MYSQL_DB: "myDb"
        depends_on:
          - mysql
      mysql:
        image: mysql:5.7
        environment:
           MYSQL_DATABASE: "myDb"
           MYSQL_USER: "admin"
           MYSQL_PASSWORD: "admin"
           MYSQL_ROOT_PASSWORD: "admin"
        ports:
          - "3306:3306"
        volumes:
          - ./message.sql:/docker-entrypoint-initdb.d/message.sql
          - mysql-data:/var/lib/mysql
    volumes:
      mysql-data:
    ```
    
    Use this Docker Compose configuration to define both services (MySQL and Flask app) and their dependencies.
    
17. 🚀 **Launch Docker Compose:**
    
    ```bash
    docker-compose up -d
    ```
    
    Start the Docker Compose services in detached mode. Docker Compose reads the configuration from `docker-compose.yml` and orchestrates the deployment.
    
18. 🛑 **Stop Docker Compose:**
    
    ```bash
    docker-compose down
    ```
    
    Stop and remove the Docker Compose services.
    

Congratulations! You've successfully set up a two-tier Flask app on Docker with detailed steps for each stage. Feel free to explore, modify, and share your experiences with others in community. Happy coding! 🚀🐳

🚀 **Connect with Me:**

If you found this tutorial helpful or have any questions, feel free to connect with me on LinkedIn and GitHub. I'm always excited to engage with the developer community!

* [LinkedIn](https://www.linkedin.com/in/ganesh-shinde-509b1366/) 🌐
    
* [GitHub](https://github.com/ganesh4400) 🐱
    

Feel free to explore more of my projects and articles. Your feedback is valuable, and I'm here to assist you on your coding journey.

Happy coding! 🚀🐱