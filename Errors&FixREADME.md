# 🚀 CI/CD + GitOps Pipeline using Jenkins, Kubernetes & Argo CD

---

## 📌 Project Overview

This project implements a **complete CI/CD pipeline integrated with GitOps**, designed to automate build, testing, security scanning, and deployment on Kubernetes.

It includes:

- Automated CI pipeline using Jenkins  
- Code quality analysis with SonarQube  
- Artifact storage using AWS S3  
- Docker image build & push to DockerHub  
- Security scanning using Trivy  
- GitOps-based deployment using Argo CD  
- Slack notifications for pipeline status  

---

## 🏗 Architecture Overview

### 🔄 CI/CD Flow


Developer → GitHub → Jenkins CI Pipeline → S3 Artifact Store
→ Docker Build & Push → DockerHub
→ Manual Approval
→ Downstream Pipeline
→ GitOps Repo Update → Kubernetes (ArgoCD)


---

### 🚀 Deployment Flow (GitOps)


Jenkins → Update Kubernetes YAML → Push to GitOps Repo
↓
Argo CD detects change → Sync → Deploy to Kubernetes


---

## 🧰 Tools & Technologies Used

### ⚙️ DevOps Stack

- Jenkins  
- Docker  
- SonarQube  
- Trivy  

### ☁️ AWS Services

- EC2  
- S3  
- IAM  

### ☸️ Kubernetes & GitOps

- Amazon EKS  
- Argo CD  

### 🔔 Integration

- Slack  
- GitHub  

---

## 🔧 CI Pipeline Stages

- Checkout Code  
- Build (Maven)  
- Test  
- SonarQube Analysis  
- Quality Gate  
- Artifact Upload (S3)  
- Docker Build  
- Trivy Scan  
- Docker Push  
- Cleanup  
- Manual Approval  

---

## 🚀 CD Pipeline (GitOps)

- Downstream pipeline triggered  
- YAML updated using `sed`  
- Changes pushed to GitOps repository  
- Argo CD syncs automatically  
- Application deployed to Kubernetes  

---

## 🔔 Slack Notifications

Integrated Slack notifications for:

- ✅ Success  
- ❌ Failure  
- ⚠️ Unstable builds  
- 🚫 Aborted builds  

---

# ⚠️ Issues Faced & Solutions

---

## ❌ 1. GitHub Authentication Failed

**Error:** Invalid username or token  
**Reason:** Password authentication deprecated  

**Solution:**

- Created Personal Access Token (PAT)  
- Added in Jenkins credentials  
- Used in pipeline  

---

## ❌ 2. Sonar Scanner Not Found

**Error:** command not found  
**Reason:** Not installed  

**Solution:**

- Installed Sonar Scanner  
- Configured in Jenkins  

---

## ❌ 3. SonarQube Project Not Visible

**Reason:** Incorrect project key or token  

**Solution:**

- Verified project key  
- Regenerated token  

---

## ❌ 4. Quality Gate Failure

**Reason:** Code issues  

**Solution:**

- Fixed issues  
- Re-ran pipeline  

---

## ❌ 5. Docker Permission Issue

**Reason:** Jenkins not in docker group  

**Solution:**


sudo usermod -aG docker jenkins
sudo systemctl restart jenkins


---

## ❌ 6. mvnw Permission Denied

**Solution:**


chmod +x mvnw


---

## ❌ 7. DockerHub Login Failed

**Reason:** Incorrect credentials  

**Solution:**

- Used Jenkins credentials  

---

## ❌ 8. Trivy Scan Issue

**Solution:**


--skip-java-db-update
--timeout 5m


---

## ❌ 9. Git Push Permission Denied

**Reason:** No repository access  

**Solution:**

- Used personal repo  
- Used GitHub token  

---

## ❌ 10. Branch Not Found

**Reason:** Incorrect branch  

**Solution:**

- Used `main` branch  

---

## ❌ 11. Slack Notification Not Working

**Reason:** Bot not added  

**Solution:**

- Enabled `botUser: true`  
- Invited bot to channel  

---

## ❌ 12. Argo CD ApplicationSet Error

**Error:** no matches for kind ApplicationSet  

**Reason:** Missing CRD  

**Solution:**

- Installed required CRD  

---

## ❌ 13. Argo CD UI Not Accessible

**Error:** ERR_CONNECTION_TIMED_OUT  

**Reason:**

- AWS Security Group blocking ports  
- Service misconfiguration  

**Mistake:**

Argo CD service was in **ClusterIP mode**, but accessed externally  

**Solution:**


kubectl edit svc argocd-server -n argocd


Changed:

- ClusterIP → NodePort  

Access using:


http://<EC2-PUBLIC-IP>:<NODEPORT>


---

## ❌ 14. NodePort Not Working

**Reason:**

- Used localhost instead of public IP  
- AWS networking restriction  

**Solution:**

- Used EC2 public IP  
- Opened port in Security Group  

---

## ❌ 15. HTTP vs HTTPS Issue

**Reason:** Argo CD runs on HTTPS  

**Solution:**

- Used `https://` instead of `http://`  

---

## ❌ 16. Port Already in Use

**Error:** address already in use  

**Solution:**

- Used different port (e.g., 9090)  

---

## ❌ 17. Partial Argo CD Installation

**Reason:** Incomplete setup  

**Solution:**

- Reinstalled Argo CD  

---

## 🎯 Key Learnings

- Debugging is critical in DevOps  
- AWS Security Groups are important  
- Always verify Kubernetes services  
- CRDs are required in Argo CD  
- Use secure credentials  
- Small mistakes can break pipelines  

---

## ✅ Final Outcome

- Fully automated CI/CD pipeline  
- GitOps deployment using Argo CD  
- Docker + security scanning integrated  
- Slack notifications working  
- End-to-end DevSecOps pipeline implemented  

---

## 🚀 Conclusion

This project demonstrates:

- CI/CD automation  
- Secure deployments  
- GitOps workflow  
- Kubernetes orchestration  

It also highlights real-world debugging and problem-solving skills.

---
