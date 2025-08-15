# Infrastructure as Code Repository

## Overview
This repository serves as the authoritative source for all infrastructure definitions supporting the `cloud-native-ai-commerce` platform. It implements GitOps principles to manage the complete deployment lifecycle through declarative configuration.

## 1️⃣ Value Proposition

### Single Source of Truth for:
- **Cluster Infrastructure**: Base Kubernetes configurations
- **Service Deployments**: Versioned manifests for microservices  
- **Environment Specifications**: Consistent dev/stage/prod definitions
- **Platform Components**: Databases, monitoring, and security

### Key Benefits:
- **Reproducible Environments**: Identical infrastructure from local to production
- **Auditability**: Complete change history with peer review
- **Disaster Recovery**: Infrastructure rebuild from versioned sources

---

## 2️⃣ Repository Structure
```text
infra/
├── .github/                  # CI/CD workflows
├── charts/                   # Helm charts
├── environments/             # Env-specific configs
│   ├── dev/
│   ├── staging/
│   └── prod/
├── modules/                  # Reusable modules
├── scripts/                  # Management utilities
├── terraform/                # Cloud provisioning
└── README.md
```
---

### 3️⃣ Enable Minikube Docker Environment
```bash
   eval $(minikube docker-env)   
```
---
### 4️⃣ Build All Service Images Locally

Navigate to each service repo and build images:
```bash
   cd ../order-service  docker build -t order-service:1.0 . \
   cd ../product-service  docker build -t product-service:1.0 .
```
---

### 5️⃣ Apply Kubernetes Manifests

From the **infra** repo:
```bash
   kubectl apply -f k8s/
```
---

🐳 Docker Build Command
-----------------------

Example for **order-service**:

```bash   
   docker build -t order-service:1.0 ../order-service
```
---

Repeat for each service, changing the tag and path accordingly.

☸️ K8s Deployment Command
-------------------------

Deploy all manifests:

```bash   
   kubectl apply -f k8s/
```
---

✅ Notes
-------

*   Ensure all services use **unique ports** in Kubernetes.
    
*   Update Docker image tags in each deployment.yml before deployment.
    
*   For remote clusters, replace minikube docker-env steps with pushes to a remote registry like DockerHub.
    

📜 License
----------

This project is licensed under the MIT License.
