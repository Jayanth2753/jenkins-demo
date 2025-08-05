# CI/CD Pipeline using Jenkins, Docker, and GitHub

This project demonstrates how to automate the build and deployment process of a Node.js application using a Jenkins CI/CD pipeline with Docker.

## 🚀 Project Overview

- A simple Node.js application is built using Docker.
- Jenkins pulls the code from GitHub, builds a Docker image, and runs the container.
- The pipeline is defined using a `Jenkinsfile`.

---

## 🔧 Tools Used

- **Jenkins** (Running in Docker)
- **Docker**
- **GitHub** (Code repository)
- **Node.js** (App runtime)

---

## 🛠️ Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/Jayanth2753/jenkins-demo.git
cd jenkins-demo
2. Dockerfile (inside the repo)
This builds the Node.js app image:

Dockerfile
Copy
Edit
FROM node:14
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "index.js"]
3. Jenkinsfile (Pipeline Script)
This automates the CI/CD process:

groovy
Copy
Edit
pipeline {
    agent any
    environment {
        IMAGE_NAME = "jayajenkins/app"
    }
    stages {
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Run Container') {
            steps {
                echo 'Running container...'
                sh 'docker run -d -p 8081:3000 $IMAGE_NAME'
            }
        }
    }
}
✅ Jenkins Setup Steps
Start Jenkins in Docker:

bash
Copy
Edit
docker run -d -p 8080:8080 -p 50000:50000 --name jenkins jenkins/jenkins:lts
Install Docker inside Jenkins container if you get docker: not found error.
(We’ll need to mount the Docker socket or install Docker manually inside the container)

Create a new Pipeline job in Jenkins:

Set Git repo URL: https://github.com/Jayanth2753/jenkins-demo.git

Jenkins will automatically detect and run Jenkinsfile

🌐 Access the Application
Once the container runs successfully:

Open browser → http://localhost:8081

📦 Example Docker Commands (Manual)
bash
Copy
Edit
docker build -t jayajenkins/app .
docker run -d -p 8081:3000 jayajenkins/app
👨‍💻 Author
D Jayanth Kumar Reddy
Project: Automate Code Deployment Using CI/CD Pipeline (GitHub Actions)
Repo: https://github.com/Jayanth2753/jenkins-demo

📌 Notes
Make sure Docker is available to Jenkins.

If you get docker: not found inside Jenkins, either:

Use Docker-in-Docker (dind) setup.

Or mount host Docker socket using -v /var/run/docker.sock:/var/run/docker.sock.
