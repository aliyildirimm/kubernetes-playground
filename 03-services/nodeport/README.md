## Goal
Observe how a Kubernetes NodePort Service works.
NodePort allows external access to your pods through a port on each node.

## What is deployed
- ReplicaSet running nginx Pods
- Service (NodePort) selecting Pods via label selector
- Label used: app=nginx-nodeport-demo

## Apply manifests
```bash
## this will create our RS.
kubectl apply -f replicaset.yaml

## now apply the service to expose your pods externally
kubectl apply -f service.yaml

## Check the service and note the NodePort assigned (e.g., 80:32496/TCP)
kubectl get svc nginx-svc-nodeport

## Get node IP addresses (Internal and External)
kubectl get nodes -o wide
```

## Accessing the Service

### 1. From outside the cluster
```bash
## Port-forward the service to access it from your local machine
kubectl port-forward service/nginx-svc-nodeport 8080:80

## Now you can curl the service from your local computer
curl http://localhost:8080

## You can also open http://localhost:8080 in your browser
```

### 2. From inside the cluster using node IPs
```bash
## Create a test pod
kubectl run test-pod-nodeip --image=curlimages/curl --rm -it --restart=Never -- sh

## Inside the pod, access using first node IP
curl http://172.19.0.5:<NODE_PORT>

## Access using second node IP
curl http://172.19.0.4:<NODE_PORT>

## Both should return the nginx welcome page
## This shows NodePort works on all nodes
```

## Cleanup
```bash
kubectl delete -f service.yaml
kubectl delete -f replicaset.yaml
```