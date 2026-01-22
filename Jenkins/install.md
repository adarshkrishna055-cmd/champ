## Install Jenkins


Step-by-step guide to installation of Jenkins https://www.jenkins.io/doc/book/installing/linux/#debianubuntu

### 1. Install Jenkins on Ubuntu (Linux)


(Create ubuntu ec2-instance using t3.micro(all traffic))


Install Java



```
sudo apt update
sudo apt install fontconfig openjdk-21-jre -y
java -version
```



```
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install jenkins -y
jenkins --version
```

Login to Jenkins using the below URL :- EX- `http://(ec2-instance-public-ip-address):8080`

  

```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
   

Click on Install suggested plugins


Start using the Jenkins 




### 2. Install Jenkins on Windows

Download java & Install java

```
https://www.oracle.com/in/java/technologies/downloads/#jdk21-windows
```


Download Jenkins & Install

`https://www.jenkins.io/download/thank-you-downloading-windows-installer-stable/`


`login and access` =====>  `localhost:8080`


-----





