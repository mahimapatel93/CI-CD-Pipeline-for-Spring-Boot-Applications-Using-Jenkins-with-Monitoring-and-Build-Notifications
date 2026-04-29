# 🚀 CI/CD + GitOps Pipeline Setup using Jenkins

---

## 📌 Overview

This project demonstrates a complete **CI/CD pipeline integrated with GitOps** using:

* Jenkins
* Docker
* SonarQube
* AWS (EC2 + S3 + IAM)
* Kubernetes (EKS)
* Argo CD
* Slack Notifications

The pipeline automates:

* Code checkout
* Build → Test → SonarQube Analysis → Quality Gate
* Artifact storage (S3)
* Docker image build & push
* Security scanning (Trivy)
* Deployment using GitOps (Argo CD)
* Slack notifications

---

## 🏗️ Architecture

```
Developer → GitHub → Jenkins CI Pipeline → S3 Artifact Store
                                      → Docker Build & Push → DockerHub
                                      → Manual Approval
                                      → Downstream Pipeline
                                      → GitOps Repo Update → Kubernetes (ArgoCD)
```

---

## ⚙️ Prerequisites

* AWS EC2 Instance
* Jenkins
* Java 21
* Maven
* SonarQube
* Docker
* Trivy
* AWS CLI
* GitHub Repository
* DockerHub Account
* Slack App
* Kubernetes Cluster (EKS)
* Argo CD

---

## 🔧 CI Pipeline Stages

* Checkout Code
* Build (Maven)
* Test
* SonarQube Analysis
* Quality Gate
* Artifact Upload (S3)
* Docker Build
* Trivy Scan
* Docker Push
* Cleanup
* Manual Approval

---

## 🚀 CD Pipeline (GitOps)

* Downstream pipeline triggered
* YAML updated using `sed`
* Changes pushed to GitOps repository
* Argo CD syncs automatically
* Application deployed to Kubernetes

---

## 🔔 Slack Notifications

Integrated Slack notifications for:

* ✅ Success
* ❌ Failure
* ⚠️ Unstable builds
* 🚫 Aborted builds

---

# ⚠️ Issues Faced & Solutions

---

## ❌ 1. GitHub Authentication Failed

**Error:** Invalid username or token
**Reason:** Password authentication deprecated
**Solution:** Used GitHub Personal Access Token (PAT)

---

## ❌ 2. Sonar Scanner Not Found

**Error:** command not found
**Reason:** Not installed
**Solution:** Installed and configured Sonar Scanner

---

## ❌ 3. SonarQube Project Not Visible

**Reason:** Incorrect project key or token
**Solution:** Verified configuration

---

## ❌ 4. Quality Gate Failure

**Reason:** Code issues
**Solution:** Fixed issues and re-ran pipeline

---

## ❌ 5. Docker Permission Issue

**Reason:** Jenkins not in docker group

**Solution:**

```
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```

---

## ❌ 6. mvnw Permission Denied

**Solution:**

```
chmod +x mvnw
```

---

## ❌ 7. DockerHub Login Failed

**Reason:** Incorrect credentials
**Solution:** Used Jenkins credentials

---

## ❌ 8. Trivy Scan Issue

**Solution:**

```
--skip-java-db-update
--timeout 5m
```

---

## ❌ 9. Git Push Permission Denied

**Reason:** No repository access
**Solution:** Used personal repo / GitHub token

---

## ❌ 10. Branch Not Found

**Reason:** Incorrect branch name
**Solution:** Used correct branch (`main`)

---

## ❌ 11. Slack Notification Not Working

**Reason:** Bot not added to channel
**Solution:** Enabled `botUser: true` and invited bot

---

## ❌ 12. Argo CD ApplicationSet Error

**Error:** no matches for kind ApplicationSet
**Reason:** Missing CRD
**Solution:** Installed required CRD

---

## ❌ 13. Argo CD UI Not Accessible

**Error:** ERR_CONNECTION_TIMED_OUT

**Reason:**

* AWS Security Group blocking ports
* Service misconfiguration

**Mistake:**
`argocd-server` service was in **ClusterIP mode**, but accessed externally

**Solution:**

```
kubectl edit svc argocd-server -n argocd
```

Updated:

* ClusterIP → NodePort

Access using:

```
http://<EC2-PUBLIC-IP>:<NODEPORT>
```

---

## ❌ 14. HTTP vs HTTPS Issue

**Reason:** Argo CD runs on HTTPS
**Solution:** Used `https` instead of `http`

---

## ❌ 15. Partial Argo CD Installation

**Reason:** Incomplete installation
**Solution:** Reinstalled Argo CD properly

---

## 🎯 Key Learnings

* Debugging is critical in DevOps
* AWS Security Groups are very important
* Always verify Kubernetes services
* CRDs are required in Argo CD
* Use secure credentials
* Small mistakes can break pipelines

---

## ✅ Final Outcome

* Fully automated CI/CD pipeline
* GitOps deployment using Argo CD
* Docker + Security scanning integrated
* Slack notifications working
* End-to-end DevSecOps pipeline implemented

---

## 🚀 Conclusion

This project demonstrates real-world DevOps practices including:

* CI/CD automation
* Secure deployments
* GitOps workflow
* Kubernetes orchestration

It also highlights practical debugging and problem-solving skills.

---
