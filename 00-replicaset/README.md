NOTE: 
You have to add labels part which will act like a key value storage in ReplicaSet Kind.

Why is this needed?
Because in replicaset we define that we want X number of replicas and to be able to provide this, we would need to be able to always check that those 2 replicas are alive.
Adding labels is the way to check for the replicasetController.

Also think like this.
Replicaset Covers pod as well.
So there is a field called spec.template.spec. Be aware that spec.template.spec is like the manifest we had for pod in 00-pod/pod.yaml.

## Steps
```bash
kubectl apply -f replicaset.yaml
kubectl get rs
```

## Self-Healing Behavior

One of the key features of ReplicaSet is its ability to automatically maintain the desired number of replicas. If a pod is deleted, the ReplicaSet controller will automatically create a new pod to replace it.

Example:
```bash
$ kubectl get pods
NAME             READY   STATUS    RESTARTS   AGE
nginx-rs-mlbpf   1/1     Running   0          13s
nginx-rs-t49ld   1/1     Running   0          13s

$ kubectl delete pod nginx-rs-t49ld
pod "nginx-rs-t49ld" deleted from default namespace

$ kubectl get pods
NAME             READY   STATUS    RESTARTS   AGE
nginx-rs-mlbpf   1/1     Running   0          49s
nginx-rs-qxsm2   1/1     Running   0          3s
```

As you can see, after deleting `nginx-rs-t49ld`, the ReplicaSet automatically created a new pod `nginx-rs-qxsm2` to maintain the desired replica count of 2.