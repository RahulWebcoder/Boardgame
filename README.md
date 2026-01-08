
# Boardgame Application – GitOps CI/CD on AWS EKS

This repository contains a Java-based Boardgame application with a **complete end-to-end CI/CD pipeline** implemented using **GitHub Actions, Amazon EKS, Amazon ECR, and Argo CD (GitOps)**.

The project demonstrates **production-style DevOps practices**, including secure authentication via **OIDC**, automated quality gates, containerization, and pull-based deployments.

---

## 🔹 Application Credit

> **Original Application Source:**  
> https://github.com/jaiswaladi246/Boardgame  
>  
> The application code is authored by the original repository owner.  
> This fork focuses on **DevOps, CI/CD, and GitOps implementation**, not application feature development.

---

## 🏗️ Architecture Overview
Developer
↓
GitHub (Application Repo)
↓
GitHub Actions (CI)

Build & Test (Maven)

Code Quality (SonarCloud)

Docker Build

Push Image → Amazon ECR (OIDC)

Update GitOps Repo
↓
GitHub (GitOps Repo)
↓
Argo CD (CD - Pull Based)
↓
Amazon EKS (Kubernetes)



---

## 🚀 Technologies Used

- **Language:** Java 17
- **Build Tool:** Maven
- **CI:** GitHub Actions
- **Code Quality:** SonarCloud
- **Containerization:** Docker
- **Registry:** Amazon ECR
- **Kubernetes:** Amazon EKS
- **CD / GitOps:** Argo CD
- **Cloud Provider:** AWS
- **Security:** GitHub OIDC (No long-lived AWS keys)

---

## 🔐 Security Highlights

- No AWS access keys stored in GitHub
- GitHub Actions authenticates to AWS using **OIDC**
- CI has **no direct cluster access**
- Kubernetes deployments are **pull-based** via Argo CD
- Git is the **single source of truth**

---

## ⚙️ CI Pipeline Details (GitHub Actions)

The CI pipeline runs on every push to `main` and performs:

1. Checkout code with full Git history
2. Setup Java 17 environment
3. Build and test application using Maven
4. Perform static code analysis using SonarCloud
5. Build Docker image
6. Push Docker image to Amazon ECR (tagged with commit SHA)
7. Update GitOps repository with the new image tag

### Key CI Configuration
- Uses **GitHub-hosted runners**
- Uses **OIDC** to assume AWS IAM role
- Image tags are immutable (commit SHA)

---

## 🔁 CD & GitOps (Argo CD)

- Argo CD is installed inside the EKS cluster
- Argo CD continuously monitors a **separate GitOps repository**
- Any change to Kubernetes manifests triggers deployment
- Auto-sync, self-heal, and prune are enabled

### GitOps Principles Followed
- No `kubectl apply` from CI
- No manual deployments
- Rollbacks are performed via Git revert
- Configuration drift is automatically corrected

---

## 🧪 Scenarios Implemented & Tested

- **Automated deployment on image update**
- **Configuration drift detection & self-healing**
- **Rollback using Git revert**
- **Manual vs Auto Sync control**
- **Secure image pull from ECR**

---

## 📂 Repository Structure

├── .github/workflows/
│ └── ci.yml # CI pipeline
├── Dockerfile
├── pom.xml
├── src/
└── README.md



> Kubernetes manifests are maintained in a **separate GitOps repository**.

---

## 🛠️ Environment Setup Summary

### AWS
- Amazon EKS cluster with managed node group
- Amazon ECR repository for container images
- IAM role configured with OIDC trust for GitHub Actions
- Worker node IAM role with ECR read permissions

### GitHub
- Application repository (this repo)
- GitOps repository for Kubernetes manifests
- GitHub Actions secrets:
  - `SONAR_TOKEN`
  - `GITOPS_TOKEN`

---

## 📌 Key Learnings & Outcomes

- Built a **secure, production-style GitOps CI/CD pipeline**
- Implemented **pull-based CD** using Argo CD
- Eliminated long-lived credentials using **OIDC**
- Improved deployment reliability and auditability
- Gained hands-on experience with real-world DevOps patterns

---

## 👤 Author

**Rahul Patel**  
DevOps / Cloud Engineer  
GitHub: https://github.com/RahulWebcoder

---

## 📄 License

This project follows the same license as the original application repository.







