
# NETFLIX KE PITAJI


## 🎯 About The Project

This project demonstrates a complete **DevOps CI/CD pipeline** for a static Netflix clone web application. The app is containerized using **Docker** with an **Nginx** web server, and automated deployment is handled via **Jenkins** running on an **Ubuntu Virtual Machine**.

> **Live Demo:** [netflix-1uh.pages.dev](https://netflix-1uh.pages.dev)


## Demo Card

[![Netflix Ke Pitaji Demo](https://raw.githubusercontent.com/pulkitpareek18/netflix/main/netflix-ke-pitaji.gif)](https://netflix-1uh.pages.dev)


Watch all your favourite movies, web series, TV shows and anime for free. 


## Demo

https://netflix-1uh.pages.dev

## GIF

![App GIF](https://raw.githubusercontent.com/pulkitpareek18/netflix/main/netflix-ke-pitaji.gif)

---

## ✨ Features

- 🎬 Watch movies, web series, TV shows and anime for free
- 🔗 URL sharing — share any movie/show link directly
- ⚡ Ultra fast loading — static site with minified assets
- 📱 PWA enabled — installable as mobile/desktop app
- 🐳 Fully containerized with Docker + Nginx
- 🔁 Automated CI/CD pipeline via Jenkins
- 🔒 Security scanning with Semgrep

---

Open the project directory and run `index.html`.


# 🎬 Netflix Ke Pitaji — CI/CD Deployment

<div align="center">

![Netflix Deploy Banner](https://raw.githubusercontent.com/pulkitpareek18/netflix/main/netflix-ke-pitaji.gif)

**A fully automated Docker + Jenkins CI/CD pipeline for deploying a Netflix-style static web app on Ubuntu VM.**

[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://hub.docker.com)
[![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white)](https://jenkins.io)
[![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)](https://nginx.org)
[![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)](https://ubuntu.com)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/RiyaDesai-2004/Netflix_Deploy)

</div>

---

## 📋 Table of Contents

- [About The Project](#about-the-project)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Docker Setup](#docker-setup)
- [Jenkins CI/CD Pipeline](#jenkins-cicd-pipeline)
- [Deployment Flow](#deployment-flow)
- [Features](#features)
- [Author](#author)

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | HTML5, CSS3, JavaScript, jQuery |
| **Web Server** | Nginx (Alpine) |
| **Containerization** | Docker |
| **CI/CD** | Jenkins |
| **Server** | Ubuntu VM |
| **Version Control** | Git + GitHub |
| **PWA** | Service Worker + Web Manifest |

---

## 📁 Project Structure

```
Netflix_Deploy/
│
├── 📁 .github/
│   └── 📁 workflows/
│       ├── ci.yml              # GitHub Actions CI
│       └── semgrep.yml         # Security scan
│
├── 📁 icons/                   # Favicons & PWA icons
│
├── 📄 index.html               # Main SPA — movie browser
├── 📄 style.css                # App styling
├── 📄 style.min.css            # Minified CSS
├── 📄 script.js                # App logic (IMDB API calls)
├── 📄 script.min.js            # Minified JS
├── 📄 jquery.js                # jQuery library
├── 📄 manifest.json            # PWA manifest
├── 📄 sw.js                    # Service Worker
├── 📄 contact.html             # Contact page
├── 📄 privacy-policy.html      # Privacy page
├── 📄 terms-and-conditions.html
├── 🐳 Dockerfile               # Docker config
├── 📄 Jenkinsfile              # Jenkins pipeline
└── 📄 README.md
```

---

## 🚀 Getting Started

### Prerequisites

Make sure you have the following installed on your Ubuntu VM:

```bash
# Docker
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker

# Java (for Jenkins)
sudo apt install fontconfig openjdk-17-jre -y

# Git
sudo apt install git -y
```

### Clone The Repository

```bash
git clone https://github.com/RiyaDesai-2004/Netflix_Deploy.git
cd Netflix_Deploy
```

---

## 🐳 Docker Setup

### Dockerfile

```dockerfile
FROM nginx:alpine
COPY . /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### Build & Run Manually

```bash
# Build image
docker build -t netflix-ke-pitaji .

# Run container
docker run -d -p 80:80 --name netflix-container netflix-ke-pitaji

# Check running containers
docker ps

# View in browser
http://YOUR_VM_IP
```

### Useful Docker Commands

```bash
# Stop container
docker stop netflix-container

# Remove container
docker rm netflix-container

# View logs
docker logs netflix-container

# Remove image
docker rmi netflix-ke-pitaji
```

---

## ⚙️ Jenkins CI/CD Pipeline

### Install Jenkins (WAR Method)

```bash
# Download Jenkins WAR
wget -O /opt/jenkins.war https://get.jenkins.io/war-stable/latest/jenkins.war

# Run Jenkins
java -jar /opt/jenkins.war --httpPort=8080
```

### Open Jenkins Dashboard

```
http://YOUR_VM_IP:8080
```

### Get Initial Password

```bash
cat ~/.jenkins/secrets/initialAdminPassword
```

### Give Jenkins Docker Permission

```bash
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```

### Jenkinsfile

```groovy
pipeline {
    agent any

    environment {
        IMAGE_NAME     = "netflix-ke-pitaji"
        CONTAINER_NAME = "netflix-container"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/RiyaDesai-2004/Netflix_Deploy.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm   $CONTAINER_NAME || true
                    docker run -d -p 80:80 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success { echo '✅ Deployment Successful!' }
        failure { echo '❌ Build Failed. Check logs.' }
    }
}
```

### Create Pipeline in Jenkins UI

```
1. Jenkins Dashboard → New Item
2. Name: netflix-deploy → Select: Pipeline → OK
3. Scroll to Pipeline section
4. Definition: Pipeline script
5. Paste the Jenkinsfile script above
6. Save → Build Now 🚀
```

---

## 🔄 Deployment Flow

```
Developer pushes code to GitHub
             ↓
    Jenkins detects changes
             ↓
    Clones latest repository
             ↓
   Docker builds nginx image
             ↓
  Old container stopped & removed
             ↓
  New container runs on port 80
             ↓
   🎬 Site is LIVE on VM IP!
```

---


## 👩‍💻 Author

**Riya Desai**

[![GitHub](https://img.shields.io/badge/GitHub-RiyaDesai--2004-181717?style=flat-square&logo=github)](https://github.com/RiyaDesai-2004)

---

## 📄 License

This project is licensed under the [MIT License](https://github.com/RiyaDesai-2004/Netflix_Deploy/blob/main/LICENSE).

---

<div align="center">
Made with ❤️ by <a href="https://github.com/RiyaDesai-2004">Riya Desai</a>
</div>
