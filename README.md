# 🚀 Spring Boot + MySQL Deployment using Kubernetes (kubeadm)

## 📌 Project Overview

This project demonstrates a complete **end-to-end DevOps workflow** for deploying a **Spring Boot application with MySQL** on a Kubernetes cluster using **kubeadm**.

It covers:

* Building a Spring Boot application
* Creating a Docker image using multi-stage build
* Pushing image to DockerHub
* Deploying MySQL using StatefulSet
* Deploying application on Kubernetes
* Automating deployment using Bash scripts

---

## 🏗️ Architecture

```
User
  ↓
NodePort Service
  ↓
Spring Boot Pod
  ↓
MySQL Service
  ↓
MySQL StatefulSet Pod
```

---

## ⚙️ Tech Stack

* Java (Spring Boot)
* Maven
* MySQL
* Docker
* Kubernetes (kubeadm)
* Bash

---

## 📂 Project Structure

```
spring_mysql_kubeadm_sakcoorg/
│
├── src/
├── pom.xml
├── Dockerfile
├── docker_build_push.sh
│
└── kube_scripts/
    ├── k8s-deploy.sh
    ├── db-statefullset-svc.yml
    ├── app-deploy-svc.yml
    ├── setup-storage.sh
```

---

# 🐳 Step 1: Build & Push Docker Image

## 🔹 Clone Repository in both master and Build nodes

```bash
git clone https://github.com/sakit333/spring_mysql_kubeadm_sakcoorg.git
cd spring_mysql_kubeadm_sakcoorg
```

---

## 🔹 Build & Push Image in build node

```bash
chmod +x docker_build_push.sh
bash docker_build_push.sh
```

### 🔍 What this script does:

* Installs Docker (if not available)
* Builds Docker image using Dockerfile
* Pushes image to DockerHub
* Removes local image

---

## ⚠️ Issue Faced

### ❌ Error:

```
Dockerfile not found
```

### ✅ Fix:

Run the script inside the project directory:

```bash
cd spring_mysql_kubeadm_sakcoorg
```

---

# ☸️ Step 2: Kubernetes Deployment in master

## 🔹 Verify Cluster

```bash
kubectl get nodes
```

Ensure all nodes are in `Ready` state.

---

## 🔹 Fix Script Path Issue (Important ⚠️)

The deployment script uses:

```bash
BASE_PATH="/kube_scripts"
```

### ❌ Issue:

Path not found

### ✅ Fix Applied:

```bash
sudo cp -r kube_scripts /kube_scripts
```

---

## 🔹 Run Deployment Script

```bash
chmod +x k8s-deploy.sh
bash k8s-deploy.sh
```

---

## 🔹 Deploy Database

Select:

```
1 → Deploy DB
```

---

## 🔹 Deploy Application

Run again:

```bash
bash k8s-deploy.sh
```

Select:

```
2 → Deploy App
```

---

# 🔍 Verification

## Check Pods

```bash
kubectl get pods
```

---

## Check Services

```bash
kubectl get svc
```

---

# 🌐 Access Application

```
http://<Worker-Node-IP>:<NodePort>
```

---

# ⚠️ Troubleshooting (Real Issues)

## ❌ Docker Build Error

* Cause: Running script outside project directory
* Fix: Navigate to correct folder

---

## ❌ Kubernetes Path Issue

* Cause: Hardcoded path in script
* Fix:

```bash
sudo cp -r kube_scripts /kube_scripts
```

---

## ❌ Pod Errors

```bash
kubectl logs <pod-name>
```

---

# 🧠 Key Learnings

* Multi-stage Docker builds
* Kubernetes StatefulSet for databases
* Service-based communication
* Real-world debugging in DevOps
* Automation using Bash scripts

---

# 🚀 Future Improvements

* Jenkins CI/CD pipeline
* GitHub webhook automation
* Ingress Controller
* Monitoring (Prometheus & Grafana)

---

# 👨‍💻 Author

**Zaid Mohammad**

---

# ⭐ Support

If you found this project useful, give it a ⭐ on GitHub!
