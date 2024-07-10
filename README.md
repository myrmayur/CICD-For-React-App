# CI/CD Pipeline Setup with Jenkins, GitHub, Docker and Kubernetes

This guide describes how to set up Jenkins on an EC2 Ubuntu server, integrate it with GitHub, and configure a Jenkins pipeline to build, test, and push a Docker image of a React.js application to DockerHub.

## Prerequisites

- AWS EC2 instance running Ubuntu
- GitHub repository containing your React.js application
- DockerHub account

## Step 1: Set Up Jenkins on EC2 Ubuntu Server

### 1.1 Update and Install Required Packages

First, update the package list and install OpenJDK:

```bash
sudo apt update
sudo apt install openjdk-11-jdk -y
```
Add Jenkins Repository and Install Jenkins
```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install jenkins -y
```
 Start and Enable Jenkins
 ```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```
Configure Firewall & allow port 8080
```bash
sudo ufw allow 8080
sudo ufw enable
sudo ufw status
```
Access Jenkins
Open your web browser and navigate to http://<your-ec2-public-ip>:8080. Follow the instructions to unlock Jenkins using the password found in:
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
## Step 2: Set Up Jenkins with GitHub Integration
# Install Required Plugins
Go to Jenkins Dashboard -> Manage Jenkins -> Manage Plugins.
Install the following plugins:
1. GitHub Integration Plugin
2. Docker Plugin
3. Pipeline Plugin
# Configure Github Integration
1. Go to Jenkins Dashboard -> Manage Jenkins -> Configure System.
2. In the GitHub section, add your GitHub credentials.
3. You may need to generate a GitHub personal access token for authentication.
## Create a Jenkins Pipeline for React.js Application
#  Create a New Pipeline Job
1. Go to Jenkins Dashboard -> New Item.
2. Select "Pipeline" and give it a name.
# Configure Pipeline
1. Select Git and provide the repository URL of your React.js application.
2. Add your GitHub credentials.
3. Checkout the Jenkinsfile present there
# Test the Jenkins Pipeline
# Run the Pipeline
1. Save the pipeline configuration and build the pipeline.
2. Jenkins will pull your React.js code, build it, create a Docker image, and push it to DockerHub.
## Deploy the Docker Image
 You can deploy the Docker image to your desired environment (e.g., another EC2 instance, Kubernetes, etc.).


## Kubernetes Deployment for Private Docker Hub Image

This repository contains the configuration files and instructions to deploy a Docker image from a private Docker Hub repository to a Kubernetes cluster.

## Prerequisites

- A Kubernetes cluster (Minikube for local development or any managed Kubernetes service like AWS EKS, GCP GKE, Azure AKS)
- `kubectl` installed and configured to interact with your Kubernetes cluster
- Docker Hub account with a private repository

## Step 1: Create a Docker Hub Secret

Create a Kubernetes secret to store your Docker Hub credentials. Run the following command, replacing `your-dockerhub-username`, `your-dockerhub-password`, and `your-email@example.com` with your Docker Hub credentials.

```sh
kubectl create secret docker-registry my-dockerhub-secret \
  --docker-username=your-dockerhub-username \
  --docker-password=your-dockerhub-password \
  --docker-email=your-email@example.com
```
Verify the secret:
```sh
kubectl get secrets
```
## Step 2: Update the Deployment YAML
Update your deployment.yaml file to use the created secret. For reference example file of a Deployment YAML is present.
## Step 3: Apply the Deployment YAML
Apply the updated Deployment YAML file to your Kubernetes cluster:
```sh
kubectl apply -f deployment.yaml
```
Verify the Deployment:
```sh
kubectl get deployments
kubectl get pods
```
## Step 4: Create a Service (Optional)
If you haven't already, create a Service to expose your Deployment. Example of a Service YAML file is present
# Apply the Service YAML file:
```sh
kubectl apply -f service.yaml
```
Verify the Service:
```sh
kubectl get services
```
## Conclusion
By following these steps, you will have a fully functional CI/CD pipeline with Jenkins, GitHub, DockerHub and Kubernetes for your React.js application on your EC2 Ubuntu server.
