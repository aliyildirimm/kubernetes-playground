## Goal
Expose an nginx ReplicaSet through a ClusterIP Service and route external HTTP traffic using an Ingress.

## Prerequisites
We need to install ingress controller first:
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
```

## Apply
```bash
kubectl apply -f rs.yaml
kubectl apply -f svc.yaml
kubectl apply -f ingress.yaml
```

## Verification
```bash
# Check ingress status
kubectl get ingress

# Access the application
curl http://localhost:80
```