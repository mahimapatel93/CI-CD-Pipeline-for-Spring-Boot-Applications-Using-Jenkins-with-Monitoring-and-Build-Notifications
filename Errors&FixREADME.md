🚀 CI/CD + GitOps Pipeline using Jenkins, Kubernetes & Argo CD
📌 Project Overview

This project implements a complete CI/CD pipeline integrated with GitOps, designed to automate build, testing, security scanning, and deployment on Kubernetes.

It includes:

Automated CI pipeline using Jenkins
Code quality analysis with SonarQube
Artifact storage using AWS S3
Docker image build & push to DockerHub
Security scanning using Trivy
GitOps-based deployment using Argo CD
Slack notifications for pipeline status
🏗 Architecture Overview
🔄 CI/CD Flow
Developer → GitHub → Jenkins CI Pipeline → S3 Artifact Store
                                      → Docker Build & Push → DockerHub
                                      → Manual Approval
                                      → Downstream Pipeline
                                      → GitOps Repo Update → Kubernetes (ArgoCD)
🚀 Deployment Flow (GitOps)
Jenkins → Update Kubernetes YAML → Push to GitOps Repo
        ↓
Argo CD detects change → Sync → Deploy to Kubernetes
🧰 Tools & Technologies Used
⚙️ DevOps Stack
Jenkins (CI Pipeline)
Docker (Containerization)
SonarQube (Code Quality)
Trivy (Security Scanning)
☁️ AWS Services
EC2 (Jenkins + Tools hosting)
S3 (Artifact Storage)
IAM (Secure Access)
☸️ Kubernetes & GitOps
Amazon EKS (Kubernetes Cluster)
Argo CD (GitOps Deployment)
🔔 Integration
Slack (Notifications)
GitHub (Source Code & GitOps Repo)
🔧 CI Pipeline Stages

The Jenkins pipeline performs:

Checkout source code from GitHub
Build application using Maven
Execute test cases
Run SonarQube analysis
Enforce Quality Gate
Upload artifact to AWS S3
Build Docker image
Scan image using Trivy
Push image to DockerHub
Cleanup unused images
Manual approval before deployment
🚀 CD Pipeline (GitOps)
Downstream pipeline triggered
Kubernetes YAML updated using sed
Changes pushed to GitOps repository
Argo CD automatically detects changes
Application deployed to Kubernetes cluster
🔔 Slack Notifications

Slack integration sends alerts for:

✅ Successful builds
❌ Failed builds
⚠️ Unstable builds
🚫 Aborted builds
⚠️ Issues Faced & Solutions
1️⃣ GitHub Authentication Failed

Error: Invalid username or token
Reason: GitHub password authentication deprecated

Fix:

Created Personal Access Token (PAT)
Stored in Jenkins credentials
Used in pipeline
2️⃣ Sonar Scanner Not Found

Error: command not found

Reason: Sonar Scanner not installed

Fix:

Installed Sonar Scanner
Configured in Jenkins
3️⃣ SonarQube Project Not Visible

Reason: Incorrect project key or token

Fix:

Verified project key
Regenerated token
4️⃣ Quality Gate Failure

Reason: Code issues (bugs/vulnerabilities)

Fix:

Fixed code issues
Re-ran pipeline
5️⃣ Docker Permission Issue

Reason: Jenkins user not added to Docker group

Fix:

sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
6️⃣ mvnw Permission Denied

Reason: Execution permission missing

Fix:

chmod +x mvnw
7️⃣ DockerHub Login Failed

Reason: Incorrect credentials

Fix:

Used Jenkins credentials securely
8️⃣ Trivy Scan Issues

Reason: Timeout / large DB download

Fix:

--skip-java-db-update
--timeout 5m
9️⃣ Git Push Permission Denied (403)

Reason: No write access to repository

Fix:

Used personal repository
Used GitHub token
🔟 Branch Not Found

Reason: Incorrect branch name

Fix:

Used correct branch: main
1️⃣1️⃣ Slack Notification Not Working

Reason: Bot not added to channel

Fix:

Enabled botUser: true
Invited bot to Slack channel
1️⃣2️⃣ Argo CD ApplicationSet Error

Error: no matches for kind "ApplicationSet"

Reason: Missing CRD

Fix:

Installed ApplicationSet CRD
Restarted controller
1️⃣3️⃣ Argo CD UI Not Accessible

Error: ERR_CONNECTION_TIMED_OUT

Root Causes:
AWS Security Group blocking ports
Wrong service type
Mistake:

Argo CD service was ClusterIP, but accessed externally

Fix:
kubectl edit svc argocd-server -n argocd

Changed:

ClusterIP → NodePort

Access using:

http://<EC2-PUBLIC-IP>:<NODEPORT>
1️⃣4️⃣ NodePort Not Working

Reason:

Tried accessing via localhost
AWS networking restrictions

Fix:

Used EC2 public IP
Opened port in Security Group
1️⃣5️⃣ HTTP vs HTTPS Issue

Reason: Argo CD runs on HTTPS

Fix:

Used https:// instead of http://
1️⃣6️⃣ Port Already in Use

Error: bind: address already in use

Reason: Port already occupied

Fix:

Used alternate port (e.g., 9090)
1️⃣7️⃣ Partial Argo CD Installation

Reason: Incomplete setup

Fix:

Reinstalled Argo CD properly
🎯 Key Learnings
Debugging is the most important DevOps skill
AWS Security Groups play a critical role
Always verify Kubernetes service types
CRDs are essential in Kubernetes-based tools
Use secure credentials (tokens, not passwords)
Small configuration mistakes can break entire pipelines
✅ Final Outcome
Fully automated CI/CD pipeline
GitOps deployment using Argo CD
Docker build + security scanning integrated
Slack notifications working
End-to-end DevSecOps pipeline implemented
🚀 Conclusion

This project demonstrates real-world DevOps practices including:

CI/CD automation
Secure deployments
GitOps workflow
Kubernetes orchestration

It also highlights strong debugging and problem-solving skills required in production environments.
