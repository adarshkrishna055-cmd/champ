## What is pod ?

A Kubernetes Pod (k8s Pod) is the smallest deployable unit in Kubernetes.

A Pod can contain one container (most common) or multiple containers.

Containers inside a Pod communicate using localhost.

Pods are ephemeral (temporary). If a Pod dies, Kubernetes creates a new Pod, not the same one.

All containers in a Pod :-

  - Share the same IP address
  - Share network ports
  - Share storage (volumes)
    

### Simple example:

* Pod = Room
* Containers = People inside the room
* They share the same space, network, and resources



## 1. vi mypodcrt.yml

```
apiVersion: v1
kind: Pod
metadata:
  name: mywebsite-pod
spec:
  containers:
  - name: website-cont1
    image: nginx:latest
    ports:
    - containerPort: 80
```


## 2. Create pod now


```
kubectl apply -f mypodcrt.yml
```


## 3. Check pod status


```
kubectl get pods
```


## 4. Check pod details


```
kubectl describe pod mywebsite-pod
```


## 5. Access pod


```
kubectl exec -it mywebsite-pod -- /bin/bash
```


## 6. Delete pod


```
kubectl delete pod mywebsite-pod
```
