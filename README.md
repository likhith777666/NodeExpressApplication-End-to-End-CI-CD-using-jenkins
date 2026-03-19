It is an Node express boilerplate application, Uisng this boilerplate implemented the CI/CD using jenkins and argocd in locally for this a tool used called minikube to run jenkins and argocd.


# 🚀 Node Express CI/CD Pipeline with Jenkins, Kubernetes & ArgoCD

## 📌 Project Overview

This project demonstrates a complete **End-to-End CI/CD pipeline** for a Node.js Express application using modern DevOps tools.

The application is containerized using Docker, deployed to Kubernetes using Minikube, and continuously delivered using Jenkins and ArgoCD.

---

## 🧰 Tech Stack

* **Backend:** Node.js, Express.js
* **Containerization:** Docker
* **CI Tool:** Jenkins
* **CD Tool (GitOps):** ArgoCD
* **Orchestration:** Kubernetes (Minikube)
* **Version Control:** GitHub

---

## ⚙️ Architecture Flow

```
Developer → GitHub → Jenkins → Docker → Docker Hub → Kubernetes → ArgoCD
```

### 🔄 Workflow Explanation

1. Developer pushes code to GitHub
2. GitHub webhook triggers Jenkins pipeline
3. Jenkins:

   * Clones repository
   * Builds Docker image
   * Pushes image to Docker Hub
4. Kubernetes manifests updated
5. ArgoCD syncs changes automatically
6. Application deployed to Kubernetes cluster

---

## 📁 Project Structure

```
.
├── src/                # Application source code
├── k8s/                # Kubernetes manifests
├── tests/              # Test cases
├── Dockerfile          # Docker build file
├── docker-compose.yml  # Local development setup
├── Jenkinsfile         # CI/CD pipeline definition
└── README.md
```

---

## 🐳 Docker Setup

### Build Image

```
docker build -t <your-dockerhub-username>/node-app .
```

### Run Container

```
docker run -p 3000:3000 <your-dockerhub-username>/node-app
```

---

## ☸️ Kubernetes Deployment

### Apply manifests

```
kubectl apply -f k8s/
```

### Check pods

```
kubectl get pods -n node-express-application
```

---

## 🔁 Jenkins Pipeline Stages

* Clone Code
* Build Docker Image
* Push Image to Docker Hub
* Deploy to Kubernetes
* Update Deployment Image

---

## 🚀 ArgoCD Setup

### Install ArgoCD

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### Access UI

```
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

### Get Admin Password (Windows PowerShell)

```
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | %{[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($_))}
```

---

## 🔗 ArgoCD Application Configuration

* **Repository URL:** Your GitHub repo
* **Path:** k8s
* **Cluster URL:** https://kubernetes.default.svc
* **Namespace:** node-express-application

---

## 🔐 Jenkins Credentials

Store Docker Hub credentials in Jenkins:

* Kind: Username & Password
* ID: `docker-creds`

Used in pipeline for secure login.

---

## ⚠️ Challenges Faced

* Docker socket permission issues in Jenkins container
* Kubernetes config conflicts between local and container
* Image pull errors in Minikube
* Path issues in kubeconfig (Windows vs Linux)

---

## ✅ Solutions Implemented

* Mounted Docker socket into Jenkins container
* Created separate kubeconfig for Jenkins
* Fixed path issues for certificates
* Used credentials binding in Jenkins pipeline

---

## 📊 Key Learnings

* End-to-end CI/CD pipeline design
* Jenkins pipeline scripting
* Kubernetes deployments & debugging
* ArgoCD GitOps workflow
* Docker image management

---

## 🔥 Future Improvements

* Add Helm charts
* Use AWS EKS instead of Minikube
* Implement monitoring (Prometheus & Grafana)
* Add automated testing stage

---

## 🙌 Author

**Likhith Nagavelli**

---

## ⭐ Support

If you like this project, give it a ⭐ on GitHub!

