# 🚀 CI/CD + GitOps Pipeline using Jenkins, Kubernetes & Argo CD

## 📌 Project Overview

This project implements a **complete CI/CD pipeline integrated with GitOps**, enabling automated build, testing, security scanning, and deployment on Kubernetes.

It includes:

- Continuous Integration using Jenkins  
- Code quality analysis using SonarQube  
- Artifact storage in AWS S3  
- Docker image build and push to DockerHub  
- Security scanning using Trivy  
- GitOps-based deployment using Argo CD  
- Slack notifications for pipeline monitoring  

---

# 🏗 Architecture Overview

## 🔄 CI/CD Flow

    Developer
        ↓
    GitHub Repository
        ↓
    Jenkins CI Pipeline
        ↓
    Build → Test → SonarQube → Quality Gate
        ↓
    Artifact Storage (S3)
        ↓
    Docker Build & Push (DockerHub)
        ↓
    Manual Approval
        ↓
    Downstream Pipeline
        ↓
    GitOps Repo Update
        ↓
    Argo CD
        ↓
    Kubernetes Deployment

---

## 🚀 GitOps Deployment Flow

    Jenkins
        ↓
    Update Kubernetes YAML (sed)
        ↓
    Push to GitOps Repository
        ↓
    Argo CD detects changes
        ↓
    Auto Sync
        ↓
    Application deployed to Kubernetes

---

# 🧰 Tools & Technologies Used

## ⚙️ DevOps Stack

- Jenkins  
- Docker  
- SonarQube  
- Trivy  

## ☁️ AWS Services

- Amazon EC2  
- Amazon S3  
- IAM  

## ☸️ Kubernetes & GitOps

- Amazon EKS  
- Argo CD  

## 🔔 Integrations

- GitHub  
- Slack Notifications  

---

# 🔧 CI Pipeline Stages

- Source Code Checkout  
- Build using Maven  
- Test Execution  
- SonarQube Analysis  
- Quality Gate Validation  
- Artifact Upload to S3  
- Docker Image Build  
- Trivy Security Scan  
- Docker Image Push  
- Cleanup  
- Manual Approval  

---

# 🔔 Notification System

Slack notifications are integrated for:

- Build Success  
- Build Failure  
- Unstable Builds  
- Aborted Builds  

---

# ⚠️ Issues Faced & Resolutions

---

## 1️⃣ GitHub Authentication Failed

### Issue
Invalid username or token  

### Root Cause
GitHub removed password-based authentication  

### Fix
- Created Personal Access Token (PAT)  
- Added in Jenkins credentials  
- Used in pipeline  

---

## 2️⃣ Sonar Scanner Not Found

### Issue
sonar-scanner: command not found  

### Root Cause
Sonar Scanner not installed  

### Fix
- Installed Sonar Scanner  
- Configured in Jenkins  

---

## 3️⃣ SonarQube Project Not Visible

### Root Cause
Incorrect project key or token  

### Fix
- Verified configuration  
- Regenerated token  

---

## 4️⃣ Quality Gate Failure

### Root Cause
Code issues (bugs/vulnerabilities)  

### Fix
- Fixed issues  
- Re-ran pipeline  

---

## 5️⃣ Docker Permission Issue

### Root Cause
Jenkins user not in Docker group  

### Fix

    sudo usermod -aG docker jenkins
    sudo systemctl restart jenkins

---

## 6️⃣ mvnw Permission Denied

### Root Cause
Execution permission missing  

### Fix

    chmod +x mvnw

---

## 7️⃣ DockerHub Login Failed

### Root Cause
Incorrect credentials  

### Fix
- Used Jenkins credentials securely  

---

## 8️⃣ Trivy Scan Issues

### Root Cause
Timeout / large database download  

### Fix

    --skip-java-db-update
    --timeout 5m

---

## 9️⃣ Git Push Permission Denied (403)

### Root Cause
No write access to repository  

### Fix
- Used personal repository  
- Used GitHub token  

---

## 🔟 Branch Not Found

### Root Cause
Incorrect branch name  

### Fix
- Used correct branch: main  

---

## 1️⃣1️⃣ Slack Notification Not Working

### Root Cause
Bot not added to Slack channel  

### Fix
- Enabled botUser: true  
- Invited bot to channel  

---

## 1️⃣2️⃣ Argo CD ApplicationSet Error

### Issue
no matches for kind "ApplicationSet"  

### Root Cause
Missing CRD  

### Fix
- Installed ApplicationSet CRD  
- Restarted controller  

---

## 1️⃣3️⃣ Argo CD UI Not Accessible

### Issue
ERR_CONNECTION_TIMED_OUT  

### Root Cause
- AWS Security Group blocking ports  
- Service misconfiguration  

### Mistake
Argo CD service was in **ClusterIP mode**, but accessed externally  

### Fix

    kubectl edit svc argocd-server -n argocd

Changed:
- ClusterIP → NodePort  

Access using:

    http://<EC2-PUBLIC-IP>:<NODEPORT>

---

## 1️⃣4️⃣ NodePort Not Working

### Root Cause
- Accessed using localhost  
- AWS networking restriction  

### Fix
- Used EC2 public IP  
- Opened ports in Security Group  

---

## 1️⃣5️⃣ HTTP vs HTTPS Issue

### Root Cause
Argo CD runs on HTTPS  

### Fix
- Used https instead of http  

---

## 1️⃣6️⃣ Port Already in Use

### Issue
Address already in use  

### Fix
- Used alternate port  

---

## 1️⃣7️⃣ Partial Argo CD Installation

### Root Cause
Incomplete installation  

### Fix
- Reinstalled Argo CD properly  

---

# 🎯 Key Learnings

- Debugging is the most critical DevOps skill  
- AWS Security Groups are essential  
- Always verify Kubernetes service types  
- CRDs are required in Argo CD  
- Use secure credentials instead of passwords  
- Small configuration mistakes can break pipelines  

---

# ✅ Final Outcome

- Fully automated CI/CD pipeline  
- GitOps-based deployment using Argo CD  
- Docker build and security scanning integrated  
- Slack notifications working  
- End-to-end DevSecOps pipeline implemented  

---

# 🚀 Conclusion

This project demonstrates real-world DevOps practices including:

- CI/CD automation  
- Secure deployments  
- GitOps workflow  
- Kubernetes orchestration  

It also highlights practical debugging and problem-solving skills in production environments.

---
