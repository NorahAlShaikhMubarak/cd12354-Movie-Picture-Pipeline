## Architecture Overview

This project implements an end-to-end CI/CD pipeline for a full-stack Movie Picture application deployed on AWS EKS using GitHub Actions.

The solution consists of:
- A **React frontend**
- A **Python (Flask) backend**
- **Dockerized services**
- **AWS ECR** for container images
- **Amazon EKS** for Kubernetes orchestration
- **GitHub Actions** for CI/CD automation

---

## High-Level System Diagram

<img width="902" height="400" alt="1-ArchitectureDiagram (1)" src="https://github.com/user-attachments/assets/4b2c52cb-d9c5-49de-99f8-536630fcadee" />

---

## CI/CD Pipeline Flow

### Frontend Continuous Deployment
1. Code is pushed or merged into the `main` branch.
2. GitHub Actions runs:
   - ESLint checks
   - Unit tests
3. A Docker image is built with environment variables injected at build time.
4. The image is pushed to Amazon ECR.
5. Kubernetes deployment is updated using `kubectl set image`.
6. The frontend is deployed to EKS and exposed via a LoadBalancer.

---

### Backend Continuous Deployment
1. Code is pushed or merged into the `main` branch.
2. GitHub Actions runs:
   - Python linting (Flake8)
   - Backend tests (Pytest)
3. A Docker image is built for the backend service.
4. The image is pushed to Amazon ECR.
5. Kubernetes backend deployment is updated in EKS.
6. The backend API becomes available to serve requests.

---

## Deployment Environment

- **Cloud Provider:** AWS  
- **Container Registry:** Amazon ECR  
- **Container Orchestration:** Amazon EKS  
- **CI/CD Tooling:** GitHub Actions  
- **Secrets Management:** GitHub Secrets  
- **Infrastructure Access:** IAM + aws-auth ConfigMap  

---

## Key Design Principles

- Automated testing before deployment
- No hardcoded credentials in pipelines
- Immutable Docker images
- Separate CI and CD concerns
- Reproducible and auditable deployments


