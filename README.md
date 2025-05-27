 # 🔁 GitOps Workflow with ArgoCD and Kubernetes

This project demonstrates a full **GitOps pipeline** using **ArgoCD** to manage Kubernetes applications via Git. All Kubernetes resources are stored in a Git repository, and ArgoCD automatically syncs and applies changes from Git to the cluster.

---

## 📌 Key Features

- ✅ **GitOps workflow** using ArgoCD
- 🚀 **Automated deployments** triggered by Git commits
- 🔒 Secure, declarative infrastructure-as-code
- 🔄 Continuous synchronization of desired state
- 🌐 Kubernetes-native application management

---

## 🛠️ Tools & Technologies

| Tool         | Purpose                            |
|--------------|-------------------------------------|
| Kubernetes   | Container orchestration platform    |
| ArgoCD       | GitOps controller                   |
| GitHub       | Git repository for manifests        |
| Docker       | Container images (e.g. NGINX)       |
| K3s/Minikube | Local Kubernetes cluster            |

---

## 📁 Project Structure

gitops-demo/
└── nginx-app/
├── deployment.yaml
└── service.yaml


---

## 🚀 Setup Instructions

### 1. 🔧 Install Prerequisites

- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Minikube](https://minikube.sigs.k8s.io/docs/) or [K3s](https://k3s.io/)
- [Git](https://git-scm.com/)
- [ArgoCD CLI (optional)](https://argo-cd.readthedocs.io/en/stable/cli_installation/)

---

### 2. 🧩 Install ArgoCD on Kubernetes

```bash
kubectl create namespace argocd

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

[kubectl get pods -n argocd]
[kubectl port-forward svc/argocd-server -n argocd 8080:443]

####Visit in your browser:
👉 https://localhost:8080

❗ Accept the security warning (self-signed certificate)

Login Credentials:
Username: admin

Password:

[kubectl get secret argocd-initial-admin-secret -n argocd \
  -o jsonpath="{.data.password}" | base64 -d && echo] >>>>>>>>>>>>> for password
4. 📦 Create Your GitOps App in ArgoCD
In the ArgoCD dashboard:

Click "New App"

Fill in the following:

Field	Value
Application Name	nginx-app
Project	default
Repository URL	https://github.com/YOUR-USERNAME/gitops-demo.git
Revision	main
Path	nginx-app
Cluster	https://kubernetes.default.svc
Namespace	default
Sync Policy	✅ Enable Auto-Sync

Click Create.

5. 🔄 GitOps Workflow in Action
>>>Make changes in your Git repo to trigger updates automatically in Kubernetes<<<<

Example: Update NGINX version
Edit deployment.yaml:

image: nginx:1.26

Commit and push:
git add .
git commit -m "Update nginx to 1.26"
git push origin main
ArgoCD auto-syncs and applies changes. Watch status update in UI 🎉

📸 Suggested Screenshots (Deliverables)
ArgoCD Dashboard (App Synced & Healthy)

App Tree View with Kubernetes objects

Auto-Sync History

Git Commit triggering update




