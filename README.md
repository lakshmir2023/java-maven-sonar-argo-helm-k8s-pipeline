# java-maven-sonar-argo-helm-k8s-pipeline

End-to-End CI/CD Pipeline for Java Application with Maven, SonarQube, Argo CD, Helm, and Kubernetes orchestration using Jenkins.

## Jenkins CICD Pipeline Setup

### Step 1: AWS EC2 Instance
Launch EC2 Instance:

Access AWS Console.
Navigate to EC2 > Instances > Launch Instance.
Follow the steps to configure the instance.

![image](https://github.com/lakshmir2023/java-maven-sonar-argo-helm-k8s-pipeline/assets/141936877/70464921-49b6-4c61-9be6-40fd2ed2d75f)
![image](https://github.com/lakshmir2023/java-maven-sonar-argo-helm-k8s-pipeline/assets/141936877/680aae96-4d2e-4426-aead-d5f82560a052)
![image](https://github.com/lakshmir2023/java-maven-sonar-argo-helm-k8s-pipeline/assets/141936877/5ea4c009-3a80-4090-88fb-8ef03d0359c1)


### Step 2: Install Jenkins
Install Java (JDK):

Connect to the EC2 instance.

Run commands to update and install OpenJDK 11.

sudo apt update<br>sudo apt install openjdk-11-jre -y

Verify Java installation.

java -version

Install Jenkins:

Add Jenkins repository key.<br>sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
  
<br>Add Jenkins repository to sources list.<br>echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
  
<br>Update and install Jenkins.<br>sudo apt-get update<br>sudo apt-get install jenkins -y

<br>Login to Jenkins:

Access Jenkins using the public IP and port 8080.Retrieve the initial admin password from the instance.

<br>sudo cat /var/lib/jenkins/secrets/initialAdminPassword

<br>Complete the Jenkins setup, install suggested plugins.Create Admin User: Create the first admin user for Jenkins.

Step 3: Install Docker Pipeline Plugin
Log in to Jenkins:
Access Jenkins dashboard.
Install Docker Pipeline Plugin:

Navigate to Manage Jenkins > Manage Plugins.
Search for "Docker Pipeline" in the Available tab.
Install the plugin and restart Jenkins.
![image](https://github.com/lakshmir2023/java-maven-sonar-argo-helm-k8s-pipeline/assets/141936877/64a29344-65c7-46c0-af26-ccbbbb5ea711)


### Step 4: Docker Slave Configuration
Install Docker on EC2 Instance:

Run commands to update and install Docker.
<br>sudo apt update<br>sudo apt install docker.io -y

Grant Permissions:
Grant Jenkins and Ubuntu users permission to the Docker daemon.
<br>sudo apt update<br>usermod -aG docker jenkins<br>usermod -aG docker ubuntu<br>systemctl restart docker

Restart Jenkins:

Restart Jenkins to apply changes.<br>http://<ec2-instance-public-ip>:8080/restart

Project Setup
Now that you have Jenkins and Docker set up, you can proceed with setting up your CI/CD pipeline for a Java application. Here are the general steps:

Create a New Jenkins Pipeline:

Define a new pipeline in Jenkins.
Use a Jenkinsfile to describe your pipeline stages.
Define Pipeline Stages:

Clone your Java application repository.
Build the application using Maven.
Integrate SonarQube for code analysis.
Build Docker image if applicable.
Deploy the application to Kubernetes using Helm and Argo CD.
Integrate Docker and Kubernetes:

Ensure Docker is integrated into your pipeline.
Use Kubernetes and Helm for deploying and managing your application.
Test and Iterate:

Test your pipeline stages.
Iterate on the Jenkinsfile and configurations.
Continuous Improvement:

Explore additional Jenkins plugins or configurations for specific needs.
Enhance your pipeline based on project requirements.
Make sure to customize the Jenkinsfile and configurations according to your project's structure and dependencies. This setup will automate your CI/CD process, providing efficient and consistent deployment of your Java application.
