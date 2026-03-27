🚀 ArgoCD Application Deployment using GitOps
<p align="center"> <img src="https://argo-cd.readthedocs.io/en/stable/assets/argo.png" width="120"/> </p> <p align="center"> <b>GitOps Continuous Delivery for 🚀 ArgoCD Application Deployment (GitOps-Based Kubernetes Deployment)
📌 Project Overview

This project demonstrates a production-ready GitOps workflow using ArgoCD to deploy applications on Kubernetes. It eliminates manual deployment errors and ensures consistent, automated, and version-controlled application delivery.

🔍 Problem Solved:
Traditional deployments are manual, error-prone, and lack traceability. This project implements GitOps principles, where Git becomes the single source of truth, enabling:

Automated deployments
Easy rollback
Improved reliability and auditability

💡 Designed to reflect real-world DevOps practices used in modern cloud-native environments.

🏗️ Architecture

This project follows a GitOps-based deployment architecture:

Developer pushes code/config → GitHub repo
ArgoCD monitors repo changes
ArgoCD syncs state → Kubernetes cluster
Application deployed automatically
🔁 Flow:
Developer → GitHub Repo → ArgoCD → Kubernetes Cluster
📊 Architecture Diagram
[ Developer ]
      |
      v
[ GitHub Repository ]
      |
      v
[ ArgoCD Controller ]
      |
      v
[ Kubernetes Cluster ]
      |
      v
[ Application Running ]

📌 (Add architecture diagram image here if available)

🧰 Tech Stack
☁️ Cloud / Infra: AWS (EC2 / EKS or Kind cluster)
☸️ Container Orchestration: Kubernetes
🚀 GitOps Tool: ArgoCD
📦 Package Manager: Helm (if used)
🐳 Containerization: Docker
🔄 CI/CD: GitHub Actions (optional/extendable)
📁 Version Control: Git & GitHub
🔄 CI/CD Workflow (GitOps)

This project follows a GitOps-driven CI/CD approach:

🔁 Pipeline Flow:
👨‍💻 Developer updates Kubernetes manifests
📤 Code pushed to GitHub
🔍 ArgoCD detects changes in repo
🔄 ArgoCD syncs desired state
🚀 Application deployed to Kubernetes
Code → Git Push → ArgoCD Sync → Kubernetes Deployment

💡 No direct kubectl usage — everything is declarative & automated.

📂 Repository Structure
argocd-application-deployment/
│
├── manifests/                # Kubernetes YAML files
│   ├── deployment.yaml      # Application Deployment
│   ├── service.yaml         # Service exposure
│
├── argocd/                  # ArgoCD application config
│   └── application.yaml     # ArgoCD app definition
│
├── README.md                # Project documentation
📌 Explanation:
manifests/ → Contains Kubernetes resources
argocd/ → Defines how ArgoCD tracks & deploys app
README.md → Documentation for setup and usage
⚙️ Setup & Installation
✅ Prerequisites
Kubernetes cluster (Kind / Minikube / EKS)
kubectl installed
ArgoCD installed
🔧 Step 1: Clone Repository
git clone https://github.com/sutar-rushikesh/argocd-application-deployment.git
cd argocd-application-deployment
🔧 Step 2: Install ArgoCD (if not installed)
kubectl create namespace argocd

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
🔧 Step 3: Access ArgoCD UI
kubectl port-forward svc/argocd-server -n argocd 8080:443
🔧 Step 4: Apply ArgoCD Application
kubectl apply -f argocd/application.yaml
🔧 Step 5: Verify Deployment
kubectl get pods
kubectl get svc
🚀 Deployment Strategy
✅ GitOps-based deployment
🔁 Auto-sync enabled via ArgoCD
📦 Declarative Kubernetes manifests
🔄 Easy rollback using Git history
✨ Key Features
🚀 Fully automated deployment using GitOps
🔄 Continuous synchronization with Git
📊 Real-time visibility via ArgoCD UI
🧩 Modular and clean repository structure
⚡ Fast and reliable deployments
🔁 Easy rollback capability
☸️ Kubernetes-native approach
📸 Screenshots / Proof

Add real screenshots to boost impact

📊 ArgoCD Dashboard
📦 Application Sync Status
☸️ Running Pods
✅ Successful Deployment
/screenshots/argocd-ui.png
/screenshots/pods-running.png
/screenshots/app-sync.png
