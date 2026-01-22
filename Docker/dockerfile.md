## Host a webapp using Dockerfile


### Launch EC2 Ubuntu Instance (Console Steps)


Choose AMI →  Ubuntu 24.04 LTS

Instance Type → t3.micro (Free Tier eligible)

Security Group → Add rules:

SSH (Port 22) → your IP

HTTP (Port 80) → anywhere (if you want web access)



### Install Docker


```
sudo apt update
sudo apt install -y docker.io
docker --version
```

```
sudo usermod -aG docker ubuntu
```

Then log out and back in so Docker permissions update.


```
mkdir mydocker
cd mydocker
```


#### A.  vi index.html


```
<!DOCTYPE html>
<html>
<head>
    <title>Docker on EC2</title>
</head>
<body>
    <h1>Hello from Docker Container</h1>
</body>
</html>

```

#### B.  vi Dockerfile


```
FROM nginx:latest

COPY index.html /usr/share/nginx/html/index.html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

```

#### C.  Build Docker Image


```
docker build -t my-nginx-app .
```

```
docker images
```

#### D.  Run Docker Container


```
docker run -d -p 80:80 --name nginx-container my-nginx-app
```

```
docker ps -a
```

Access it using browser.


#### E.  Go Inside the Running Container


```
docker exec -it nginx-container /bin/bash
```


#### F.  Create a New File Inside Container


```
cd /usr/share/nginx/html
touch newfile.txt
echo "This file was created inside container" > newfile.txt
ls
```



=======END========


