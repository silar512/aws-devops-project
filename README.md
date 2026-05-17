# aws-devops-project
AWS Infrastructure Deployment & Monitoring System

A production-style DevOps project demonstrating cloud infrastructure deployment, Docker containerization, Nginx reverse proxy configuration, CI/CD automation using GitHub Actions, and infrastructure monitoring concepts on AWS.

⸻

Live Demo

🌐 Live Application: http://16.171.40.224

⸻

Project Overview

This project demonstrates how modern cloud-native applications are deployed and managed using AWS cloud infrastructure and DevOps tools.

The application is hosted on an AWS EC2 Ubuntu server, containerized using Docker, served through Nginx, and automated using GitHub Actions CI/CD workflows.

⸻

Architecture

GitHub Repository
        ↓
GitHub Actions CI/CD
        ↓
AWS EC2 Ubuntu Server
        ↓
Docker Container
        ↓
Nginx Reverse Proxy
        ↓
Portfolio Website

⸻

Technologies Used

Cloud Platform

* AWS EC2
* AWS IAM
* AWS CloudWatch
* AWS VPC

Operating Systems

* Ubuntu Linux
* Linux Administration

DevOps Tools

* Docker
* Git
* GitHub
* GitHub Actions
* Nginx

Programming & Scripting

* HTML
* CSS
* Bash

⸻

Features

* Deployed containerized web application on AWS EC2
* Configured Docker-based application deployment
* Implemented Nginx reverse proxy configuration
* Configured Linux server administration workflows
* Automated deployment pipeline using GitHub Actions
* Publicly hosted cloud application
* Infrastructure troubleshooting and monitoring workflows
* Production-style DevOps architecture

⸻

Project Setup

1. Launch AWS EC2 Instance

* Create Ubuntu EC2 instance
* Configure security groups:
    * Port 22 (SSH)
    * Port 80 (HTTP)
    * Port 443 (HTTPS)

⸻

2. Connect to EC2

chmod 400 john.pem
ssh -i john.pem ubuntu@YOUR_PUBLIC_IP

⸻

3. Update Ubuntu Server

sudo apt update
sudo apt upgrade -y

⸻

4. Install Docker

sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker

Verify:

docker --version

⸻

5. Install Nginx

sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx

Verify:

sudo systemctl status nginx

⸻

Docker Setup

Dockerfile

FROM nginx:latest
COPY . /usr/share/nginx/html

⸻

Build Docker Image

docker build -t myapp .

⸻

Run Docker Container

docker run -d -p 8080:80 myapp

⸻

Nginx Reverse Proxy Configuration

Edit:

sudo nano /etc/nginx/sites-available/default

Configuration:

server {
    listen 80;
    server_name _;
    location / {
        proxy_pass http://localhost:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}

Restart Nginx:

sudo systemctl restart nginx

⸻

GitHub Actions CI/CD

Workflow File

Location:

.github/workflows/deploy.yml

Workflow:

name: Deploy
on:
  push:
    branches:
      - main
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: SSH Deploy
      uses: appleboy/ssh-action@master
      with:
        host: ${{ secrets.EC2_HOST }}
        username: ${{ secrets.EC2_USERNAME }}
        key: ${{ secrets.EC2_SSH_KEY }}
        script: |
          cd /home/ubuntu/aws-devops-project
          git pull
          docker stop mycontainer || true
          docker rm mycontainer || true
          docker build -t myapp .
          docker run -d --name mycontainer -p 8080:80 myapp

⸻

GitHub Secrets

Configured repository secrets:

Secret Name	Description
EC2_HOST	AWS EC2 Public IP
EC2_USERNAME	Ubuntu username
EC2_SSH_KEY	Private PEM key

⸻

Linux Commands Used

sudo systemctl status nginx
sudo systemctl restart nginx
sudo docker ps
sudo docker images
sudo docker logs CONTAINER_ID
sudo docker stop CONTAINER_ID
sudo docker rm CONTAINER_ID
sudo apt update
sudo apt install docker.io

⸻

Troubleshooting

Docker Permission Issue

Solution:

sudo usermod -aG docker ubuntu

Reconnect SSH after running the command.

⸻

Nginx Default Page Showing

Solution:

* Configure proper reverse proxy
* Restart Nginx service

sudo systemctl restart nginx

⸻

GitHub Authentication Failed

Solution:

* Use GitHub Personal Access Token (PAT)
* Password authentication is deprecated

⸻

Future Improvements

* HTTPS SSL configuration
* Custom domain integration
* Terraform Infrastructure as Code
* Kubernetes deployment
* Monitoring dashboards
* Load balancer setup
* Auto Scaling configuration
* Blue-Green deployment strategy

⸻

Skills Demonstrated

* Linux Administration
* AWS Cloud Infrastructure
* Docker Containerization
* Nginx Configuration
* CI/CD Automation
* GitHub Actions
* Infrastructure Troubleshooting
* DevOps Workflow Management
* Reverse Proxy Configuration
* Cloud Deployment

⸻

Resume Highlights

* Deployed containerized applications on AWS EC2 using Docker
* Implemented CI/CD automation using GitHub Actions
* Configured Nginx reverse proxy for production deployment
* Managed Linux cloud infrastructure environments
* Performed deployment troubleshooting and operational support
* Built cloud-hosted DevOps portfolio project

⸻

Author

Shaik Silar

* GitHub: https://github.com/silar512
* LinkedIn: https://linkedin.com/in/shaiksilar
* Email: shaiksilar.cloud@gmail.com

⸻

License

This project is created for educational and portfolio purposes.
