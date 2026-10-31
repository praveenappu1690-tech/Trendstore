# Trendstore – Application Deployment (DevOps Project)

## 1. Project Overview

This project demonstrates the deployment of a React-based Trendstore application into a production-ready environment using DevOps tools and AWS services.

The application is deployed using Docker and Kubernetes (AWS EKS), with Terraform for infrastructure provisioning and Jenkins for CI/CD automation.

## 2. Application Details

- **Application:** Trendstore
- **Source Repository:** https://github.com/Vennilavanguvi/Trend.git
- **GitHub Repository:** https://github.com/praveenappu1690-tech/Trendstore
- **Application Port:** 3000
- **Deployment Platform:** AWS EC2 and Amazon EKS

## 3. Technologies Used

| Tool | Purpose |
|---|---|
| AWS EC2 | Virtual server |
| Terraform | Infrastructure provisioning |
| Docker | Application containerization |
| Docker Hub | Docker image storage |
| Amazon EKS | Kubernetes cluster |
| Kubernetes | Application deployment |
| Jenkins | CI/CD automation |
| Git & GitHub | Version control |
| Prometheus | Application availability monitoring |
| Blackbox Exporter | HTTP health checks |
| Grafana | Monitoring dashboard |
| Nginx | Web server |

## 4. Project Structure

```text
Trendstore/
│
├── dist/                  # Production application files
├── terraform/             # Terraform configuration
├── k8s/                   # Kubernetes YAML files
│   ├── deployment.yaml
│   └── service.yaml
├── monitoring/             # Monitoring configuration
│   ├── prometheus.yml
│   └── blackbox.yml
├── screenshots/            # Project evidence
├── Dockerfile
├── nginx.conf
├── Jenkinsfile
├── .gitignore
├── .dockerignore
└── README.md
```

## 5. Infrastructure Setup

- Created AWS EC2 instances for project setup and deployment.
- Installed Git, Docker, Jenkins, AWS CLI, kubectl and Terraform.
- Configured AWS infrastructure using Terraform.
- Created an Amazon EKS cluster.
- Verified the cluster status.

## 6. Docker Deployment

- Created a Dockerfile to containerize the Trendstore application.
- Built the Docker image.
- Tested the application using a Docker container.
- Verified application accessibility through the browser.
- Created a Docker Hub repository and pushed the application image.

Build command:

```bash
docker build -t trend-store:1.0 .
```

## 7. Kubernetes Deployment

- Created Kubernetes Deployment and Service YAML files.
- Configured application replicas.
- Created a Kubernetes LoadBalancer service.
- Configured kubectl to communicate with the EKS cluster.
- Deployed the application to Kubernetes.

## 8. Jenkins CI/CD Pipeline

Configured Jenkins with the required plugins and GitHub integration.

The pipeline is designed to automate:

1. GitHub source code checkout.
2. Application validation.
3. Docker image build.
4. Docker Hub image push.
5. EKS deployment using kubectl.
6. Deployment verification.

Jenkins pipeline execution logs are included in the screenshots folder.

## 9. Monitoring Setup

Configured open-source monitoring tools to monitor the Trendstore application.

- **Prometheus:** Collects monitoring metrics.
- **Blackbox Exporter:** Checks application HTTP availability.
- **Grafana:** Provides a visual monitoring dashboard.

Monitoring endpoints:

- Prometheus: `http://EC2-PUBLIC-IP:9090`
- Grafana: `http://EC2-PUBLIC-IP:3001`
- Application: `http://EC2-PUBLIC-IP:3000`

Verified that the Trendstore target is UP in Prometheus.

## 10. Application Access

The application can be accessed through the deployed application endpoint.

**Application URL:** `http://EC2-PUBLIC-IP:3000`

**Kubernetes LoadBalancer DNS:** Add your EKS Service LoadBalancer endpoint here.

**LoadBalancer ARN:** Add the AWS LoadBalancer ARN here, if required by the submission.

## 11. Screenshots and Evidence

The `screenshots/` directory contains project execution evidence, including:

- AWS EC2 instance creation.
- Terraform execution.
- EKS cluster status.
- Docker image build.
- Docker Hub repository.
- Kubernetes deployment and service.
- Jenkins pipeline execution console output.
- External application endpoint.
- Prometheus monitoring targets.
- Grafana monitoring dashboard.

## 12. Conclusion

Successfully configured the Trendstore application deployment environment using AWS, Terraform, Docker, Kubernetes and Jenkins.

Implemented application availability monitoring using Prometheus and Blackbox Exporter, with Grafana for monitoring visualization.

This project demonstrates practical experience with cloud infrastructure, containerization, Kubernetes deployment, CI/CD automation and application monitoring.

---
