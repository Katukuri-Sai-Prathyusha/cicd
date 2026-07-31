# 🚀 CI/CD Pipeline using Jenkins, Docker, GitHub & AWS EC2

## 📌 Project Overview

This project demonstrates a complete **Continuous Integration and Continuous Deployment (CI/CD)** pipeline for a **NestJS** application using **GitHub**, **Jenkins**, **Docker**, and **AWS EC2**.

Whenever code is pushed to the GitHub repository, Jenkins automatically retrieves the latest source code, builds a Docker image, and deploys the updated application by replacing the existing container.

This project also includes real-world troubleshooting such as resolving memory issues, disk space limitations, Docker deployment errors, and AWS networking configuration.

---

# 🏗️ Architecture

```text
                 Developer
                     │
                 Git Push
                     │
                     ▼
          GitHub Repository
                     │
                     ▼
         Jenkins Pipeline (EC2)
                     │
                     ▼
      Checkout Latest Source Code
                     │
                     ▼
         Build Docker Image
                     │
                     ▼
      Stop Previous Container
                     │
                     ▼
      Start New Docker Container
                     │
                     ▼
         NestJS Application
                     │
                     ▼
        http://<EC2-Public-IP>:3000
```

---

# 🛠️ Technologies Used

* AWS EC2 (Ubuntu 24.04)
* Jenkins
* Docker
* Git & GitHub
* Node.js
* NestJS
* Linux
* Bash
* SSH

---

# 📁 Project Structure

```
.
├── src/
├── test/
├── Dockerfile
├── Jenkinsfile
├── package.json
├── tsconfig.json
├── README.md
└── .dockerignore
```

---

# ⚙️ CI/CD Workflow

1. Developer pushes code to GitHub.
2. Jenkins detects the latest code (Pipeline from SCM).
3. Jenkins checks out the repository.
4. Docker builds a new application image.
5. Existing container is stopped and removed.
6. A new container is started using the latest image.
7. The updated application becomes available on port **3000**.

---

# 🐳 Dockerfile

The Docker image is built using the official Node.js Alpine image.

Main steps:

* Create working directory
* Copy package files
* Install dependencies
* Copy source code
* Build NestJS application
* Expose port 3000
* Start the application

---

# 🔧 Jenkins Pipeline

The Jenkins pipeline performs the following stages:

### Build Docker Image

```bash
docker build -t cicd-app .
```

### Stop Existing Container

```bash
docker stop cicd-app || true
docker rm cicd-app || true
```

### Deploy Latest Container

```bash
docker run -d --name cicd-app -p 3000:3000 cicd-app
```

---

# 🚀 Deployment

The application is deployed inside a Docker container running on an AWS EC2 Ubuntu instance.

Application URL:

```
http://<EC2-Public-IP>:3000
```

---

# 📋 Prerequisites

Before running this project, install:

* Git
* Docker
* Jenkins
* Node.js
* Java 21
* AWS EC2 Ubuntu instance

---

# ▶️ Running the Project Locally

Clone the repository:

```bash
git clone <repository-url>
cd cicd
```

Install dependencies:

```bash
npm install
```

Run the application:

```bash
npm run start
```

Development mode:

```bash
npm run start:dev
```

---

# 🐳 Running with Docker

Build the image:

```bash
docker build -t cicd-app .
```

Run the container:

```bash
docker run -d --name cicd-app -p 3000:3000 cicd-app
```

Verify:

```bash
curl http://localhost:3000
```

---

# 🔍 Troubleshooting

During implementation, several real-world issues were encountered and resolved.

## 1. Jenkins Out of Memory

**Problem**

The Jenkins service was terminated by the Linux OOM Killer while building the Docker image.

**Solution**

* Created a 1 GB swap file.
* Restarted Jenkins successfully.

---

## 2. Root Volume Full

**Problem**

The EC2 root volume reached 99% utilization, preventing Jenkins from starting.

**Solution**

* Increased the EBS root volume from 8 GB to 30 GB.
* Expanded the partition using `growpart`.
* Resized the filesystem using `resize2fs`.

---

## 3. Application Not Accessible

**Problem**

The application worked locally but was inaccessible from the internet.

**Solution**

Added an inbound Security Group rule to allow TCP traffic on port **3000**.

---

## 4. Git Checkout Issue

**Problem**

Jenkins attempted an unnecessary second Git checkout.

**Solution**

Removed the duplicate checkout stage because Jenkins Pipeline from SCM already performs the checkout.

---

# 📈 Skills Demonstrated

* CI/CD Pipeline Design
* Jenkins Pipeline
* Docker Containerization
* AWS EC2 Administration
* Git & GitHub Integration
* Linux System Administration
* Docker Image Creation
* Bash Scripting
* Troubleshooting Production Issues
* AWS Security Groups
* Storage Expansion (EBS)
* Memory Management (Swap)

---

# 🚀 Future Improvements

* Configure GitHub Webhooks for automatic builds.
* Push Docker images to Docker Hub or Amazon ECR.
* Implement multi-stage Docker builds.
* Deploy using Kubernetes.
* Configure Nginx as a reverse proxy.
* Enable HTTPS with Let's Encrypt.
* Add monitoring and alerting using Prometheus and Grafana.

---

# 📚 Key Learning Outcomes

This project provided practical experience in building an end-to-end CI/CD pipeline, automating deployments with Jenkins, containerizing applications using Docker, deploying applications on AWS EC2, and troubleshooting common infrastructure issues such as memory exhaustion, storage limitations, and network configuration.

---

# 👤 Author

**Sai Prathyusha**

DevOps | AWS | Docker | Jenkins | Linux | Git | CI/CD
