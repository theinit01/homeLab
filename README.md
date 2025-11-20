# 🏡 homeLab — ArgoCD Manifests

This repository contains Kubernetes manifests and ArgoCD application configurations intended to be deployed via ArgoCD to a small home lab running on a 2-node `k3s` cluster.

**Cluster specifics**
- Cluster type: `k3s` (2 nodes)
- CNI: `Cilium`
- Storage: `Longhorn` (block/PV provisioner)

## 🚀 Purpose
This repo is focused on ArgoCD-driven GitOps for the homelab. Manifests and ArgoCD Application definitions here target a lightweight homelab cluster and are designed to be managed by ArgoCD rather than applied manually. Workloads include media stack, monitoring, `n8n`, Traefik, and related components configured for Cilium networking and Longhorn storage.

## 🗂️ Notable folders
```
n8n/               # n8n manifests (namespace, deployment, service, postgres secret)
traefik/           # Traefik deployment + service
media-stack/       # Jellyfin, Radarr, Sonarr, qBittorrent, etc.
monitoring/        # Uptime-Kuma and other lightweight monitoring
authentik/         # Authentication components
cloudflared/       # Cloudflared daemonset (optional)
```

## ⚙️ Prerequisites
- A running k3s cluster with 2 nodes
- `kubectl` configured to point at the cluster
- Cilium installed as the cluster CNI
- Longhorn installed for persistent volumes

Install examples (cluster operator may prefer different versions):

Install Cilium (quick apply):
```
kubectl apply -f https://raw.githubusercontent.com/cilium/cilium/main/install/kubernetes/quick-install.yaml
```

Install Longhorn (default YAML):
```
kubectl apply -f https://raw.githubusercontent.com/longhorn/longhorn/master/deploy/longhorn.yaml
```

Verify your cluster and that the CNI and storage are ready before deploying workloads:
```
kubectl get nodes
kubectl -n kube-system get pods
kubectl -n longhorn-system get pods
```

## 🖥️ Node hardware (this homelab)
- Nodes: 2
- Model: `Lenovo ThinkCentre M920q`
- CPU: `Intel Core i3` (8th Gen)
- Memory: `16 GB` RAM per node

## 🔁 Deploying the manifests
You can apply everything in the repo (or specific folders) once prerequisites are satisfied.

Apply all manifests recursively from the repo root:
```
kubectl apply -R -f .
```

Or apply a single component, e.g. `n8n`:
```
kubectl apply -R -f n8n/
```

## Notes
- Ensure Longhorn storage class is set as the default (or set PVC storageClassName explicitly in manifests).
- Cilium should be installed before pods that rely on CNI networking come up.