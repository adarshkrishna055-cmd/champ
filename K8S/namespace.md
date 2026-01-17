## Namespace

In Kubernetes (k8s), a Namespace is a logical partition used to organize, isolate, and manage resources within a cluster.

A Namespace is like a folder inside a Kubernetes cluster that separates resources.

Default namespaces exist by default.

You can have:

* `dev` namespace → development apps
* `test` namespace → testing apps
* `prod` namespace → production apps

### Simple analogy :-

* Kubernetes Cluster = Building
* Namespace = Floor
* Pods/Services = Rooms on that floor

### Why Namespaces are used:

 - Organize resources (dev, test, prod)
 - Avoid name conflicts (same resource names can exist in different namespaces)
 - Better cluster management for large environments


### Default Kubernetes namespaces:

* **default** – resources created without specifying a namespace
* **kube-system** – Kubernetes system components
* **kube-public** – public data (mostly read-only)
* **kube-node-lease** – node heartbeat information

                 

### Command:

```
kubectl get namespaces
```

Create a namespace:

```
kubectl create namespace dev
```



## How to create pod inside default namespace ?


```
vi default-namespace-pod-crt.yml
```


```
apiVersion: v1
kind: Pod
metadata:
  name: pod1
spec:
  containers:
  - name: container1
    image: nginx
    ports:
    - containerPort: 80

```


```
kubectl apply -f default-namespace-pod-crt.yml
```

```
kubectl get pods
```

```
kubectl get pod pod1 -o wide

```



### How to create pod inside custom namespace ?



```
kubectl create namespace custons
```

```
kubectl get ns
```


```
vi custom-namespace-pod-crt.yml
```


```
apiVersion: v1
kind: Pod
metadata:
  name: pod2
  namespace: custons
spec:
  containers:
  - name: container2
    image: nginx
    ports:
    - containerPort: 81

```


```
kubectl apply -f mypodcrt.yml
```


--------------------------------------------------


