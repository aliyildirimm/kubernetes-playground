## Goal
Understand how a Kubernetes Deployment manages Pods and ensures desired state.

## What is deployed
- Object: Deployment
- Replicas: 2
- Image: nginx

## Steps
```bash
kubectl apply -f deployment.yaml
kubectl get deployment

# You will see that deployment under the hood creates a replicaset
kubectl get rs

## same for the pods
kubectl get pods