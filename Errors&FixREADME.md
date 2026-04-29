

## ⚠️ Issues Faced & Solutions

---

### ❌ 1. GitHub Authentication Failed

**Error:** Invalid username or token

**Reason:** Password auth deprecated

**Solution:** Used GitHub PAT

---

### ❌ 2. Sonar Scanner Not Found

**Error:** command not found

**Reason:** Not installed

**Solution:** Installed & configured


---

### ❌ 3. SonarQube Project Not Visible

**Reason:** Wrong key/token

**Solution:** Verified configuration

---

### ❌ 4. Quality Gate Failure

**Reason:** Code issues

**Solution:** Fixed and re-run

---

### ❌ 5. Docker Permission Issue

**Reason:** Jenkins not in docker group

**Solution:**

```
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```

---

### ❌ 6. mvnw Permission Denied

**Solution:**

```
chmod +x mvnw
```

---

### ❌ 7. DockerHub Login Failed

**Reason:** Wrong credentials

**Solution:** Used Jenkins credentials

---

### ❌ 8. Trivy Scan Issue

**Solution:**

```
--skip-java-db-update
--timeout 5m
```

---

### ❌ 9. Git Push Permission Denied

**Reason:** No repo access

**Solution:** Used personal repo / token

---

### ❌ 10. Branch Not Found

**Solution:** Used correct branch (`main`)

---

### ❌ 11. Slack Not Working

**Reason:** Bot not added

**Solution:** Enabled botUser + invited bot

---

### ❌ 12. Argo CD ApplicationSet Error

**Error:** no matches for kind ApplicationSet

**Reason:** Missing CRD

**Solution:** Installed CRD

---

### ❌ 13. Argo CD UI Not Accessible

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

Changed:

* ClusterIP → NodePort

Then accessed using:

```
http://<EC2-PUBLIC-IP>:<NODEPORT>
```

---

### ❌ 16. HTTP vs HTTPS Issue

**Reason:** Argo CD uses HTTPS

**Solution:** Used `https`

---

### ❌ 17. Partial Argo CD Installation

**Reason:** Incomplete install

**Solution:** Reinstalled properly

---

### ❌ 18. Repository Fork Issue

**Solution:** Deleted fork, created new repo

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

