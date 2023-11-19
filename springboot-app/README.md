# Spring Boot based Java web application
 
This is a simple Sprint Boot based Java application that can be built using Maven. Sprint Boot dependencies are handled using the pom.xml at the root directory of the repository.

This is a MVC architecture based application where controller returns a page with title and message attributes to the view.

## Execute the application locally and access it using your browser

Checkout the repo and move to the directory

```
git clone https://github.com/lakshmir2023/java-maven-sonar-argo-helm-k8s-pipeline.git/
cd java-maven-sonar-argocd-helm-k8s-pipeline/sprintboot-app
```

Execute the Maven targets to generate the artifacts

```
sudo apt install maven -y
mvn clean package
```

The above maven target stores the artifacts to the `target` directory. You can either execute the artifact on your local machine
(or) run it as a Docker container.

** Note: To avoid issues with local setup, Java versions and other dependencies, I would recommend the docker way. **


### Execute locally (Java 11 needed) and access the application on http://localhost:8080

```
java -jar target/spring-boot-web.jar
```

### The Docker way

Build the Docker Image

```
docker build -t ultimate-cicd-pipeline:v1 .
```

```
docker run -d -p 8010:8080 -t ultimate-cicd-pipeline:v1
```

Hurray !! Access the application on `http://<ip-address>:8010`
![Alt text](image-1.png)

## Next Steps

### Configure a Sonar Server locally

```
apt install unzip
adduser sonarqube
sudo su - sonarqube
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.4.0.54424.zip
unzip sonarqube-9.4.0.54424.zip
chmod -R 755 /home/sonarqube/sonarqube-9.4.0.54424
chown -R sonarqube:sonarqube /home/sonarqube/sonarqube-9.4.0.54424
cd sonarqube-9.4.0.54424/bin/linux-x86-64/
./sonar.sh start
```

Hurray !! Now you can access the `SonarQube Server` on `http://<ip-address>:9000` 

The default username and password is admin

How Jenkins will authenticate SonarQube?
<br>Go to sonar > In profile > My Account > Security > provide token name and generate it > click on copy button
![image](https://github.com/lakshmir2023/java-maven-sonar-argo-helm-k8s-pipeline/assets/141936877/9f288b02-4d05-45cf-8e70-0642ab06383c)

Go to Jenkins > Manage Jenkins > Manage Credentials > System > Global credentials > Add credentials

![image](https://github.com/lakshmir2023/java-maven-sonar-argo-helm-k8s-pipeline/assets/141936877/518b4c68-6017-4745-b9e0-0c67fa1f81ca)

Open command prompt or git bash (local terminal)

Install and start minikube using docker or hyperkit

minikube documentation - https://minikube.sigs.k8s.io/docs/start/
<br>Youtube link - https://youtu.be/vZuyr9bmcks?feature=shared

Start minikube 

minikube start

Installation of Argo CD<br>
https://operatorhub.io/operator/argocd-operator

To install Argo CD follow the given steps in operators hub.


