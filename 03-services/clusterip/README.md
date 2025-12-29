## ClusterIP Service

### Amaç
ClusterIP servisi, pod'lara sadece cluster içinden erişim sağlar. Bu, internal microservices communication için kullanılır.

### Özellikler
- Sadece cluster içinden erişilebilir
- Sabit bir cluster IP adresi alır
- Pod'lar arası load balancing yapar
- Service name ile DNS üzerinden erişilebilir

## Apply manifests
```bash
## this will create our RS.
kubectl apply -f replicaset.yaml
## now apply the service to expose your pods
kubectl apply -f service.yaml


# now you can see the IP for your service:
# there is also svc-name which can be used in the cluster as well. You don't need to 
# hardcode the ip in the code, using service name makes it more clear.
kubectl get svc nginx-svc

# you can also list the endpoints:
kubectl get endpoints nginx-svc

# Cluster içinden test (başka bir pod'dan)
kubectl run test-pod --image=curlimages/curl --rm -it --restart=Never -- curl http://nginx-svc

# Veya port-forward ile local'den erişim
kubectl port-forward service/nginx-svc 8080:80
curl http://localhost:8080

# to clean up
kubectl delete -f service.yaml
kubectl delete -f replicaset.yaml
```