## Goal
Observe how a Kubernetes Service works.
You can also call like an INTERNAL LOAD BALANCER.

## What is deployed
- ReplicaSet running nginx Pods
- Service (ClusterIP) selecting Pods via label selector
- Label used: app=nginx-svc-demo

## Apply manifests
```bash
## this will create our RS.
kubectl apply -f replicaset.yaml

## you will see that pods have IP.
kubectl get pods -o wide

##now delete the rs and reapply
kubectl delete rs nginx-rs-svc-demo
kubectl apply -f replicaset.yaml

# if you check for the pods you will realize that IPs exists yes but they are different than before. So we need service that always has the same IP and acts like a load balancer for our pods.
kubectl get pods -o wide

## now apply the service to expose your pods
kubectl apply -f service.yaml


# now you can see the IP for your service:
# there is also svc-name which can be used in the cluster as well. You don't need to 
# hardcode the ip in the code, using service name makes it more clear.
kubectl get svc nginx-svc

# you can also list the endpoints:
kubectl get endpoints nginx-svc

#however if you try to curl from local you will be unsuccessful but if you enter the cluster it will work. But then how can you? That's the topic we can discuss in INGRESS. For now we can simply port-forward and access to the service.
# Port-forward the service to access it from your local machine:
kubectl port-forward service/nginx-svc 8080:80

# Now you can curl the service from your local computer:
# This should return the default nginx welcome page.
# You can also open http://localhost:8080 in your browser.
curl http://localhost:8080

