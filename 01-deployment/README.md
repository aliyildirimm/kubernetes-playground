## Goal
Understand how a Kubernetes Deployment manages Pods and ensures desired state.

## What is deployed
- Object: Deployment
- Replicas: 2
- Image: nginx
- Label: app=nginx-demo

## Steps
```bash
kubectl apply -f manifests/deployment.yaml
kubectl get deployment
kubectl get rs
kubectl get pods