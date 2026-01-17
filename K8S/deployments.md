## Deployment


A Kubernetes Deployment is a resource used to deploy, manage, and scale Pods automatically.

A Deployment tells Kubernetes how many Pods to run, which container image to use, and how to update them.

### Why Deployment is used:

 - Keeps Pods running all the time
 - Automatically **recreates Pods** if they fail
 - Supports **scaling** (up/down)
 - Supports **rolling updates & rollbacks**

### Key components:

* **Deployment** → manages
* **ReplicaSet** → ensures required Pod count
* **Pods** → run containers

### What Deployment does:

* Maintains desired number of Pods
* Replaces failed Pods automatically
* Updates Pods with zero/minimal downtime
* Allows rollback to previous versions

### Simple example:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```

### Useful commands:

Create deployment:

```bash
kubectl apply -f deployment.yaml
```

Check deployment:

```bash
kubectl get deployments
```

Scale deployment:

```bash
kubectl scale deployment nginx-deploy --replicas=5
```

Update image:

```bash
kubectl set image deployment/nginx-deploy nginx=nginx:1.25
```

Rollback:

```bash
kubectl rollout undo deployment nginx-deploy
```

------------------------------------
