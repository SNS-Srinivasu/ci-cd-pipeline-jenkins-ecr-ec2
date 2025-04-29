# CI/CD Pipeline Using Jenkins, ECR, and EC2

# Architecture 


<img width="1375" alt="Screenshot 2025-04-30 at 1 53 27 AM" src="https://github.com/user-attachments/assets/79892702-cd8b-4071-a37a-1697f322604b" />

# Jenkins Master & Slave

<img width="1440" alt="Screenshot 2025-04-29 at 4 38 28 PM" src="https://github.com/user-attachments/assets/5ee82e85-2db6-434f-ada2-72d3635b615e" />

# ECR Repositories 

 <img width="1440" alt="Screenshot 2025-04-29 at 5 19 14 PM" src="https://github.com/user-attachments/assets/ca11fae1-ba0a-460c-b5e6-fc7d295fc4f3" />

# Image Pushed To ECR

<img width="1440" alt="Screenshot 2025-04-29 at 5 19 23 PM" src="https://github.com/user-attachments/assets/71202c33-1c21-41ab-9a2a-c4ba194a9166" />

# Deployed to Server

<img width="1440" alt="Screenshot 2025-04-29 at 6 33 53 PM" src="https://github.com/user-attachments/assets/2c5334ad-e2f0-4b5d-8c00-55718aefcbde" />

# Jenkins Builds

<img width="1440" alt="Screenshot 2025-04-29 at 6 32 00 PM" src="https://github.com/user-attachments/assets/3ebc6dd8-f8c0-4087-b1c0-395a392908cc" />

# Application

<img width="1440" alt="Screenshot 2025-04-29 at 6 34 38 PM" src="https://github.com/user-attachments/assets/097e377b-b389-42cc-9fe8-325cdac8bd60" />



## 📘 Project Description

This project showcases a Dockerized CI/CD pipeline built using **Jenkins**, **Amazon ECR**, and **EC2** instances. The pipeline is fully automated: any code change pushed to GitHub triggers a Jenkins pipeline that builds a Docker image, pushes it to ECR, and deploys it to a remote EC2 instance running the application in a Docker container.

---

## 🏗️ Infrastructure Overview

The CI/CD system runs across **three EC2 instances**:

### 1️⃣ Jenkins Master (EC2 Instance 1)
- Runs Jenkins inside a Docker container.
- Listens for GitHub webhook triggers.
- Orchestrates the pipeline and delegates build jobs to the Jenkins Agent.

### 2️⃣ Jenkins Agent (EC2 Instance 2)
- Connects to Jenkins Master.
- Performs tasks like:
  - Cloning the GitHub repository
  - Building a Docker image using the `Dockerfile`
  - Pushing the Docker image to AWS ECR

### 3️⃣ Deployment Server (EC2 Instance 3)
- Pulls the latest image from ECR using `docker pull`.
- Stops and removes the old container if it exists.
- Runs the new container exposing the app on **port 8081**.
- Serves static content using **Nginx** or a Node-based server via `app.js`.

---

## 🔁 CI/CD Pipeline Flow

1. ✅ Developer pushes code to GitHub.
2. 🔔 GitHub Webhook notifies Jenkins.
3. ⚙️ Jenkins pipeline runs:
   - Jenkins Agent clones the repo.
   - Builds Docker image using `Dockerfile`.
   - Pushes image to AWS ECR.
4. 🚀 Jenkins SSHs into Deployment EC2:
   - Logs into ECR
   - Pulls latest image
   - Removes previous container
   - Runs updated app container on port `8081`.

---

## 📁 Repository Structure

```bash
.
├── Dockerfile        # Builds image for the app
├── Jenkinsfile       # Jenkins CI/CD pipeline script
├── app.js            # Node.js app (optional if serving via Nginx)
├── index.html        # Static web page
├── style.css         # Styling for index.html
└── README.md         # Project documentation
