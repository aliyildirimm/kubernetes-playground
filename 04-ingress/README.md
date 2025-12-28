## Goal
Expose an nginx ReplicaSet through a ClusterIP Service and route external HTTP traffic using an Ingress.

## Apply
```bash
kubectl apply -f rs.yaml
kubectl apply -f svc.yaml
kubectl apply -f ingress.yaml


# how to verify part is missing, I should be able to provide better local development



## we need to install ingress controller running:
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml


# now just check
kubectl get ingress

# then go to
localhost:80