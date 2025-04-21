# DevOps Pipeline on AWS
This project demonstrates a production-ready DevOps deployment pipeline built from the ground up using:
- **AWS EKS** for container orchestration
- **Terraform** for infrastructure as code
- **Docker** for containerization
- **GitHub Actions** for CI/CD automation
- **CloudWatch** for centralized logging and monitoring
- **Kubernetes** for deployment and secret management

---

## Project Highlights
- Infrastructure provisioning with scalable VPC and EKS using Terraform
- Containerized Node.js application with Docker
- Secure configuration using Kubernetes Secrets
- Continuous delivery pipeline via GitHub Actions
- End-to-end observability using AWS CloudWatch

---

## Deployment Guide (New AWS Account)

### Prerequisites
- AWS CLI, kubectl, Terraform, and Docker installed
- Access to an AWS account with EKS/IAM permissions
- GitHub & Docker Hub accounts

### 1. Clone the Repository
```bash
git clone https://github.com/xinyi-tony-liu/DevOps.git
cd DevOps
```

### 2. Provision Infrastructure with Terraform
```bash
cd infra
terraform init
terraform apply
```

### 3. Configure kubeconfig for EKS
```bash
aws eks --region us-east-1 update-kubeconfig --name devops-eks
```

### 4. Create Kubernetes Secret
```bash
kubectl create secret generic app-secret \
  --from-literal=GREETING="Hello with your secret"
```

### 5. Trigger Deployment via GitHub Actions
Push any code change to the `main` branch to trigger CI/CD.

### 6. Access the Deployed Application
```bash
kubectl get svc hello-world-service
```
Use the external IP in a browser.

---

## Architecture Overview
- **Terraform** provisions VPC, subnets, and EKS resources
- **Kubernetes** manages application deployments, scaling, and secrets
- **GitHub Actions** automates image build, push, and cluster updates
- **CloudWatch** aggregates metrics and logs from EKS pods and services

---

## Monitoring and Alerting
- Metrics available in **CloudWatch > Container Insights**
- Logs streamed via Fluent Bit
- Alerts can be configured using **CloudWatch Alarms** and **SNS** email notifications

---

## Project Structure
```
.
├── app/           # Node.js app source
├── infra/         # Terraform infrastructure modules
├── k8s/           # Kubernetes manifests
├── .github/       # CI/CD workflows
│   └── deploy.yml
└── Dockerfile
```

---

## Design Decisions

- **EKS over other orchestrators** for native AWS integration and scalability
- **Terraform** used instead of AWS CDK to keep the setup widely compatible
- **Kubernetes Secrets** used for simplicity, AWS Secrets Manager would work as well
- **GitHub Actions** chosen for its native integration with GitHub and ease of setup

---

## Author
Developed and maintained by [xinyitonyliu](https://github.com/xinyi-tony-liu)