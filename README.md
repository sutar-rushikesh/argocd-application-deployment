# 🚀 ArgoCD Application Deployment (GitOps)

## Overview
Deploy applications using ArgoCD via UI, CLI and Declarative GitOps approach.

## Theory
- UI & CLI = Imperative
- Declarative = GitOps

## Steps
- UI Deployment (NGINX)
- CLI Deployment (Apache)
- Declarative Deployment

## Testing
- Change replicas
- Observe sync

## Commands
argocd app list
argocd app sync

## Destroy
kind delete cluster --name argocd-cluster
