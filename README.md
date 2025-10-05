@"
# DevOps Web Application - Experiment 8

**Experiment 8:** Building a CI/CD Pipeline using Docker and Jenkins

## 🎯 Project Overview

A simple web application demonstrating complete CI/CD pipeline:
- HTML/CSS/JavaScript static website
- Dockerized with Nginx web server
- Automated builds with Jenkins
- Published to Docker Hub

## 🛠️ Technologies Used

- **Jenkins**: Automation server for CI/CD
- **Docker**: Containerization platform  
- **Nginx**: Web server
- **GitHub**: Version control
- **Docker Hub**: Container registry
- **HTML/CSS/JavaScript**: Web application

## 🚀 Quick Start

### Pull and run the latest image:
``````bash
docker pull karna1312/devops-web-app:latest
docker run -d -p 8080:80 karna1312/devops-web-app:latest
