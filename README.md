
# 🎨 Frontend Deployment Pipeline

A streamlined pipeline for deploying frontend applications (React, Vue or similar) using Docker, CI/CD workflows and automated deployment to a remote server.

## 🧰 Tech Stack

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)  
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)  
![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=white)  
![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)

---

## 📌 Overview

This repository sets up:

- Build and test pipeline for your frontend app  
- Docker multi-stage build (build + serve)  
- Automated CI/CD (push on main triggers build → image → deploy)  
- Deployment to remote server (Droplet/VPS)  
- Reverse-proxy and HTTPS routing (with Nginx or Traefik)  

---

## 🚀 Quick Start

### 1. Clone the repo  
```bash
git clone https://github.com/tysker/schoolhack-deployment-pipeline.git
cd schoolhack-deployment-pipeline
````

### 2. Configure environment (if needed)

Create a `.env` file with variables like:

```
DOCKER_HUB_USER=<your_dockerhub_user>
DOCKER_HUB_REPO=<your_repo_name>
DOMAIN=<your_domain>
```

### 3. Build & deploy locally

```bash
docker build -t yourapp-ui .
docker run -p 80:80 yourapp-ui
```

### 4. CI/CD workflow

Push to `main` branch → GitHub Actions builds & tests → builds Docker image → pushes to Docker Hub → deploys to your server automatically.

---

## 🖼️ Architecture Diagram

```
Developer → GitHub Repo
     ↓
GitHub Actions → build & test → docker image → push
     ↓
Remote Server (VPS) ← docker pull → container runs
     ↓
Browser users → Nginx/Traefik → your UI application
```

---

## 📄 Pipeline Details

* Multi-stage Dockerfile: build phase (Node) + serve phase (Nginx)
* `docker-compose.yml` for local dev & `docker-compose.prod.yml` for production
* GitHub Actions workflow file `.github/workflows/deploy.yml`
* Environment variables managed via GitHub Secrets and `.env`
* Optional: rollback strategy, version tagging

---

## 🧪 Testing & Linting

In your frontend project directory:

```bash
npm install
npm run lint
npm run test
npm run build
```

CI ensures build succeeds and tests pass before deploying.

---

## ⚠️ Notes & Considerations

* Ensure your domain’s DNS record points to your server
* Make sure port 80/443 are open on the remote server
* Keep your Docker Hub credentials and secrets safe
* For production: use secure image tags (no `latest`) and monitor container health

---

## 📜 License

MIT License — see the `LICENSE` file for details.

---
