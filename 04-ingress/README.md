## Goal
Expose an nginx ReplicaSet through a ClusterIP Service and route external HTTP traffic using an Ingress.

## Apply
```bash
kubectl apply -f rs.yaml
kubectl apply -f svc.yaml
kubectl apply -f ingress.yaml


# how to verify part is missing, I should be able to provide better local development