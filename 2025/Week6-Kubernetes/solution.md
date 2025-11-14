 Week 6 Challenge - DevOps Batch 9: Kubernetes Basics & Advanced

## 📋 Challenge Overview
Completed all Kubernetes tasks demonstrating comprehensive container orchestration skills.

## 🏗️ Architecture & Implementation

### Cluster Setup
- **Tool**: kind (Kubernetes in Docker)
- **Nodes**: 4-node cluster (1 control-plane, 3 workers)
- **Namespace**: `bank-app` for application isolation

### Application Stack
- **Frontend**: Nginx Deployment with 3 replicas
- **Database**: MySQL StatefulSet with persistent storage
- **Monitoring**: DaemonSet for node-level monitoring
- **Networking**: Services, Ingress, Network Policies
- **Security**: RBAC with Admin, Developer, Tester roles

## 📁 Kubernetes Manifest Files

All manifest files are located in the `k8s-manifests/` directory:

- **Core Objects**: pod.yml, deployment.yaml, statefulset.yaml, daemonset.yaml
- **Networking**: nginx-service.yaml, nginx-nodeport.yaml, mysql-service.yaml, nginx-ingress.yaml, network-policy.yaml
- **Storage**: static-pv.yaml, static-pvc.yaml
- **Security**: mysql-secret.yaml, serviceaccounts.yaml, roles.yaml, rolebindings.yaml
- **Autoscaling**: nginx-hpa.yaml
- **Advanced**: database-backup-job.yaml, daily-cleanup-cronjob.yaml, bankapp-crd.yaml, my-bankapp-instance.yaml

## 🔧 Key Commands Executed

```bash
# Cluster setup
kind create cluster --name bankapp --config cluster.yml

# Application deployment
kubectl apply -f namespace.yml
kubectl apply -f deployment.yaml
kubectl apply -f mysql-statefulset.yaml

# Networking
kubectl apply -f nginx-service.yaml
kubectl apply -f nginx-nodeport.yaml

# Autoscaling
kubectl apply -f nginx-hpa.yaml

# Security
kubectl apply -f serviceaccounts.yaml,roles.yaml,rolebindings.yaml

# Verification
kubectl get all -n bank-app
kubectl get hpa -n bank-app
