# Flask + Nginx + ArgoCD GitOps Deployment

## Overview
GitOps deployment using Helm chart synced by ArgoCD. App: Flask behind Nginx.

## Prerequisites
- Docker Hub account (update image in values.yaml)
- Kubernetes cluster with ArgoCD installed (e.g., minikube + argocd)
- GitHub repo (fork/push this)
- argocd CLI + kubectl access

## Step-by-Step Deployment (From Scratch)

### 1. Build & Push Docker Image
```bash
docker build -t docker.io/yams0325/ci-cd:latest .
docker push docker.io/yams0325/ci-cd:latest
```
*Update `helm-chart/values.yaml` with your image.tag if changed.*

### 2. Git Setup & Push
```bash
git init
git add .
git commit -m "Add Helm chart for ArgoCD GitOps"
git branch -M main
git remote add origin https://github.com/yourusername/argocicd.git  # Your repo
git push -u origin main
```

### 3. ArgoCD Repo & App
Login to ArgoCD: `argocd login <server> --username admin --password <pass>`
```bash
# Add Git repo
argocd repo add https://github.com/yourusername/argocicd.git

# Update argocd-app.yaml with your repoURL, then apply
kubectl apply -f argocd-app.yaml -n argocd
```

### 4. Verify
```bash
argocd app list
argocd app get flask-app
kubectl get pods,svc -n flask
kubectl port-forward svc/flask-app 8080:80 -n flask  # curl localhost:8080
```
Expected: "Flask + Nginx + ArgoCD Pipeline Working!"

## Customization
- Scale: Edit values.yaml replicaCount → git push → ArgoCD syncs.
- Production: Change service.type=LoadBalancer, add Ingress.
- Update image: values.yaml → git push.

## Original Manifests
Backed up in `k8s-backup/`.
