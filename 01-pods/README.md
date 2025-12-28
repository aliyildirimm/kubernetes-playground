## Goal
Run a single Pod.

## Steps
```bash
# Create the pod from the YAML file
kubectl apply -f pod.yaml

# View the pod status with extended information (node, IP, readiness)
kubectl get pod nginx-pod -o wide

# Show detailed information about the pod including events and conditions
## this would also show the events happend until the container started succesfully.
kubectl describe pod nginx-pod

# if you want to remove:
kubectl delete pods nginx-pod