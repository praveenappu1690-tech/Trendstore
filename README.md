# Trend Application — AWS DevOps Deployment

## 1. Project Overview

This project demonstrates the deployment of a React application using **Docker, Terraform, AWS, Jenkins, DockerHub, Amazon EKS, Kubernetes, and CI/CD**.

The application is containerized and deployed on AWS with an automated deployment workflow.

---

## 2. Architecture

```text
Developer
   ↓
GitHub
   ↓
Jenkins
   ↓
Docker Build
   ↓
DockerHub
   ↓
Amazon EKS
   ↓
Kubernetes
   ↓
LoadBalancer
   ↓
Browser
```

---

## 3. Repository Structure

```text
Trend/
├── dist/
├── Dockerfile
├── terraform/
├── k8s/
├── Jenkinsfile
├── README.md
└── .gitignore
```

* **dist/** – Production application files
* **Dockerfile** – Docker image configuration
* **terraform/** – AWS infrastructure configuration
* **k8s/** – Kubernetes deployment and service files
* **Jenkinsfile** – CI/CD pipeline configuration
* **README.md** – Project documentation

---

## 4. Application

The application is a React-based web application.

The production files are available in the `dist/` directory and are served using Nginx.

---

## 5. Docker

A Dockerfile is created to containerize the application.

Main steps:

```bash
docker build -t trend-app .
docker run -d -p 3000:80 --name trend-app trend-app
```

The application can be tested using:

```text
http://<EC2-PUBLIC-IP>:3000
```

---

## 6. Terraform

Terraform is used to automate AWS infrastructure provisioning.

Example resources include:

* VPC
* Subnets
* Security Groups
* EC2
* IAM
* EKS-related infrastructure

Terraform commands:

```bash
terraform init
terraform plan
terraform apply
```

---

## 7. AWS EC2

An Amazon EC2 instance is used for DevOps activities such as:

* Installing Docker
* Building Docker images
* Testing the application
* Installing Jenkins and required tools
* Connecting to AWS services

Port **3000** is allowed in the EC2 Security Group for application testing.

---

## 8. Jenkins

Jenkins is used to automate the CI/CD process.

The Jenkins pipeline performs tasks such as:

1. Checkout source code
2. Build Docker image
3. Login to DockerHub
4. Push Docker image
5. Deploy the application

---

## 9. DockerHub

The Docker image is pushed to DockerHub for container image storage.

Example:

```bash
docker login
docker tag trend-app:latest <dockerhub-username>/trend-app:latest
docker push <dockerhub-username>/trend-app:latest
```

---

## 10. EKS

Amazon EKS is used to run the application using managed Kubernetes.

The EKS cluster provides the environment required to deploy and manage application containers.

---

## 11. Kubernetes

Kubernetes manages the application containers running in EKS.

Main Kubernetes resources:

* Deployment
* Service
* Pods
* ReplicaSets

Example commands:

```bash
kubectl get nodes
kubectl get pods
kubectl get services
kubectl get deployments
```

---

## 12. CI/CD

The CI/CD workflow automates application deployment.

```text
GitHub
   ↓
Jenkins
   ↓
Docker Build
   ↓
DockerHub
   ↓
Kubernetes / EKS
   ↓
Application
```

This reduces manual deployment steps and provides a repeatable deployment process.

---

## 13. Monitoring

Application and infrastructure status can be checked using AWS and Kubernetes tools.

Useful commands:

```bash
kubectl get pods
kubectl get nodes
kubectl get svc
kubectl describe pod <pod-name>
kubectl logs <pod-name>
```

Jenkins console output can also be used to monitor pipeline execution.

---

## 14. Deployment URL

After successful deployment, the application can be accessed using the Kubernetes LoadBalancer URL:

```text
http://<LOAD-BALANCER-URL>
```

---

## 15. Commands

### Docker

```bash
docker ps
docker images
docker build -t trend-app .
docker run -d -p 3000:80 trend-app
```

### DockerHub

```bash
docker login
docker push <dockerhub-username>/trend-app:latest
```

### Kubernetes

```bash
kubectl get nodes
kubectl get pods
kubectl get svc
kubectl apply -f k8s/
kubectl delete -f k8s/
```

### Terraform

```bash
terraform init
terraform plan
terraform apply
terraform destroy
```

---

## 16. Screenshots

The project documentation includes screenshots of:

* Application running on EC2
* Docker image
* DockerHub repository
* Terraform resources
* Jenkins pipeline
* EKS cluster
* Kubernetes pods
* Kubernetes service
* LoadBalancer URL
* Final application

---

## 17. Troubleshooting

Common issues and solutions:

### Docker container stopped

```bash
docker ps -a
docker logs <container-name>
```

### Kubernetes pod issue

```bash
kubectl get pods
kubectl describe pod <pod-name>
kubectl logs <pod-name>
```

### Service not accessible

```bash
kubectl get svc
```

Check the LoadBalancer status and AWS Security Group rules.

### Jenkins pipeline failure

Check the Jenkins **Console Output** for the failed stage and verify DockerHub credentials and required permissions.

---

## Conclusion

This project demonstrates a complete DevOps deployment workflow using **GitHub, Jenkins, Docker, DockerHub, Terraform, AWS EC2, Amazon EKS, Kubernetes, and CI/CD**, from application source code to a production-style deployment.
