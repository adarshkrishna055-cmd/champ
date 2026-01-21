## Minikube Project: Deploy a Web App with Kubernetes


## Objective

To deploy a containerized web application on a local Kubernetes cluster using Minikube, expose it as a service, and access it from a browser.


## Tools Used

* Minikube
* kubectl
* Docker
* Kubernetes (Deployment, Service)




## Step 1: Start Minikube


```
sudo apt update
sudo apt install docker.io -y
```

```
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
```

```
sudo usermod -aG docker $USER && newgrp docker
```

```
sudo reboot
```

```
minikube start --driver=docker
```

```
sudo snap install kubectl --classic
```


Check cluster status:

```
kubectl get nodes
```


## Step 2: Create Deployment (Nginx)

Create a file deployment.yaml

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
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

Apply deployment:

```
kubectl apply -f deployment.yaml
```

Verify:

```
kubectl get deployments
kubectl get pods
```

---

## Step 3: Expose Deployment as a Service

Create service.yaml

```
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30007
```

Apply service:

```
kubectl apply -f service.yaml
```

Check service:

```
kubectl get svc
```


## Step 4: Access the Application

```
minikube service nginx-service
```

Nginx welcome page will open in browser.



## Step 5: Scaling the Application

```
kubectl scale deployment nginx-deployment --replicas=4
kubectl get pods
```



## Step 6: Pod & Logs Check

```
kubectl describe pod <pod-name>
kubectl logs <pod-name>
```



## Step 7: Cleanup

```
kubectl delete -f deployment.yaml
kubectl delete -f service.yaml
minikube stop
```




----------------------------
