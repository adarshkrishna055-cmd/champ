## Volume

In Kubernetes (k8s), a Volume is a way to store and share data used by containers in a Pod.

A k8s Volume allows data to persist and be shared, even if a container restarts.

Volumes are attached at the Pod level.

All containers in the same Pod can share the same volume.

Volume lifecycle is tied to the Pod, not the container.

### Why volumes are needed:

 - Container file systems are temporary
 - Data is lost when a container stops
 - Volumes keep data safe across container restarts


### Common Kubernetes volume types:

1. **emptyDir**

* Created when Pod starts
* Deleted when Pod is removed
* Used for temporary data
* Example: cache, shared files

2. **hostPath**

* Mounts a directory from the node
* Mostly used for testing
* Not recommended for production

3. **configMap**

* Stores configuration files
* Used to inject configs into Pods

4. **secret**

* Stores sensitive data (passwords, tokens)
* Data is base64 encoded

5. **PersistentVolume (PV)**

* Actual storage in the cluster
* Provided by admin or cloud provider

6. **PersistentVolumeClaim (PVC)**

* Request for storage by a Pod
* Pod uses PVC, PVC binds to PV

### Simple analogy:

* Pod = Laptop
* Volume = Hard Disk
* Container = Applications


## how to use k8s-volume



`vi myk8svoluse.yml`


```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 2Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
  persistentVolumeReclaimPolicy: Retain

---

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests: 
      storage: 300Mi

---

apiVersion: v1
kind: Pod
metadata:
  name: pvc-use-pod
spec:
  containers:
  - name: cont1
    image: nginx:latest
    command: [ "sh", "-c", "echo 'hii all i m ram' > /data/mydata.txt && sleep 3600" ]
    volumeMounts:
    - mountPath: /data
      name: my-datastorage
  volumes:
  - name: my-datastorage
    persistentVolumeClaim:
      claimName: my-pvc

```


```
kubectl apply -f myk8svoluse.yml
```


```
kubectl get pod pvc-use-pod
```


#### go inside pod and check your data


```
kubectl exec -it pvc-use-pod -- sh
```

```
cat /data/mydata.txt
```




------------------------------------------------------


