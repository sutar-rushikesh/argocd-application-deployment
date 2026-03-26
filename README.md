🚀 ArgoCD Application Deployment using GitOps






📌 Overview

This project demonstrates end-to-end application deployment using ArgoCD on Kubernetes following GitOps principles.

It covers three real-world approaches:

🔹 UI-based Deployment (NGINX)
🔹 CLI-based Deployment (Apache)
🔹 Declarative GitOps Deployment (Recommended)
🧠 Theory (Core Concepts)
🔸 What is ArgoCD?

ArgoCD is a declarative GitOps continuous delivery tool for Kubernetes.

👉 It continuously:

Monitors Git repository
Compares desired vs actual state
Automatically syncs changes
🔸 What is GitOps?

GitOps means:

Git = Single Source of Truth

All infrastructure & application configs are stored in Git and automatically applied.

🔸 Deployment Approaches Comparison
Approach	Type	GitOps	Use Case
UI	Imperative	❌ No	Quick testing
CLI	Imperative	❌ No	Automation scripts
Declarative	Declarative	✅ Yes	Production (Best Practice)

<img width="880" height="517" alt="image" src="https://github.com/user-attachments/assets/35916427-67b4-404b-9e81-e3e01eba4863" />
<img width="1258" height="579" alt="image" src="https://github.com/user-attachments/assets/7df6d19f-ecb8-4025-b7d4-da676f09f385" />

🔍 Flow Explanation
Developer pushes code to GitHub
ArgoCD continuously watches the repo
Detects changes in manifests
Applies them to Kubernetes cluster
Ensures cluster state = Git state
⚙️ Prerequisites

Before starting, ensure:

✅ Kubernetes Cluster (Kind / EKS / AKS)
✅ ArgoCD Installed
✅ kubectl configured
✅ Git repository with manifests
✅ ArgoCD CLI installed
🚀 Implementation Steps
🔹 1. UI-Based Deployment (NGINX)
📌 Steps
Login to ArgoCD UI
Click New App
Provide:
Repo URL
Path: ui_approach/nginx
Cluster & Namespace
📷 Output
Application created via UI
Manual sync required

👉 Observation:

Easy but not GitOps compliant
🔹 2. CLI-Based Deployment (Apache)
📌 Command
argocd app create apache-app \
  --repo https://github.com/<your-repo>.git \
  --path cli_approach/apache \
  --dest-server https://<cluster-endpoint> \
  --dest-namespace default \
  --sync-policy automated \
  --self-heal \
  --auto-prune
📌 Key Flags Explained
Flag	Meaning
--sync-policy automated	Auto deploy changes
--self-heal	Fix manual drift
--auto-prune	Remove unused resources

👉 Observation:

Faster than UI
Still not fully GitOps (manual trigger)
🔹 3. Declarative GitOps Deployment (Best Practice) ✅
📌 Create Application YAML
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: nginx-app
spec:
  destination:
    namespace: default
    server: https://kubernetes.default.svc
  source:
    repoURL: https://github.com/<your-repo>.git
    path: declarative/nginx
    targetRevision: HEAD
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
📌 Apply
kubectl apply -f application.yaml

👉 Observation:

Fully GitOps
Production-ready approach
🧪 Testing (Real DevOps Scenario)
🔹 Test Case 1: Scaling
Update replicas in Git
Commit changes
ArgoCD detects change
Sync automatically

👉 Result: Pods scale automatically

🔹 Test Case 2: Drift Detection
Delete pod manually:
kubectl delete pod <pod-name>
ArgoCD auto recreates it

👉 Result: Self-healing works

🔁 Self-Healing & Auto-Sync
✅ Features Demonstrated
Drift detection
Auto-sync from Git
Self-healing of deleted resources
Auto-pruning unused resources
🌐 Application Access

From your setup:

NGINX → http://<EC2-IP>:8081
Apache → http://<EC2-IP>:8082

👉 Verified:

✅ NGINX running
✅ Apache running
🧾 Common ArgoCD CLI Commands
Command	Description
argocd login <server>	Login to ArgoCD
argocd app list	List apps
argocd app get <app>	App details
argocd app sync <app>	Sync app
argocd app delete <app>	Delete app
argocd cluster list	Show clusters
⚠️ Issues Faced & Fixes
❌ Issue:
InvalidSpecError: cluster not found
✅ Fix:
Corrected cluster URL
Verified using:
argocd cluster list
📊 Key Learnings
Difference between Imperative vs Declarative
Real GitOps workflow
ArgoCD architecture
Self-healing mechanism
Production deployment strategies
🧨 Cleanup
kind delete cluster --name argocd-cluster

👨‍💻 Author

Rushikesh Sutar

