# 🏡 Homelab Infrastructure

This repository contains my **Homelab setup**, built and deployed on a **Kind cluster with 3 nodes**.  
It leverages modern DevOps tools to manage applications, networking, and observability in a self-hosted environment.  

## 🚀 Overview
The homelab includes:
 - **ArgoCD** → GitOps-based deployment and application lifecycle management
 - **Traefik** → Reverse proxy and ingress controller for traffic routing
 - **Prometheus** → Metrics collection and monitoring
 - **Grafana** → Dashboards for observability and visualization
 - **Flask Backend** → A Python web backend running on the cluster

## 🗂️ Repository Structure
```
.
├── argocd/          # ArgoCD installation manifests/configs
├── traefik/         # Traefik setup (IngressRoutes, middlewares, etc.)
├── monitoring/      # Prometheus + Grafana configs
├── flask-backend/   # Sample Flask application + manifests
└── README.md
```

## ⚙️ Setup Instructions

### Prerequisites
- A running **Kind cluster with 3 nodes**
- `kubectl` and `helm` installed locally
- (Optional) A domain name pointing to your ingress

### Installation

1. **Install ArgoCD**
  ```
    kubectl create namespace argocd
    kubectl apply -n argocd -f argocd/install.yaml
```

## 📊 Monitoring
- Prometheus scrapes metrics from the cluster and workloads
- Grafana provides visualization dashboards for nodes, workloads, and the Flask backend

## 🛠️ Future Improvements
- CI/CD pipeline integration
- Add persistent storage for Prometheus & Grafana
- Automate SSL with Let’s Encrypt
- Expand Flask backend into microservices
$ 👉 Feel free to fork this repo, suggest improvements, or use it as a reference for your own homelab!
