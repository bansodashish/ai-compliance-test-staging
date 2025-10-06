# Sample App - Staging Environment

This repository contains Kubernetes manifests for the sample application in the **staging** environment.

## 📁 Repository Structure
```
test_staging/
├── deployment.yaml     # Main application deployment
├── README.md          # This file
└── .gitignore         # Git ignore file
```

## 🏗️ Deployment Details

### **Environment**: Staging
### **Namespace**: `staging`
### **Application**: `sample-app-staging`

### **Configuration:**
- **Replicas**: 2 (for testing)
- **Image**: nginx:1.21-alpine
- **Resources**: 
  - CPU: 100m request, 200m limit
  - Memory: 128Mi request, 256Mi limit
- **Environment Variables**:
  - `ENVIRONMENT=staging`
  - `LOG_LEVEL=debug`

### **Services:**
- **ClusterIP Service**: `sample-app-service` on port 80
- **Ingress**: `sample-app-staging.example.com`

## 🚀 Deployment Commands

```bash
# Create namespace
kubectl create namespace staging

# Apply manifests
kubectl apply -f deployment.yaml

# Check deployment status
kubectl get pods -n staging
kubectl get svc -n staging
kubectl get ingress -n staging
```

## 🔍 Monitoring & Debugging

```bash
# View logs
kubectl logs -n staging deployment/sample-app-staging

# Describe pod
kubectl describe pod -n staging -l app=sample-app

# Port forward for local testing
kubectl port-forward -n staging svc/sample-app-service 8080:80
```

## ⚠️ Security Notice

**This deployment currently lacks security contexts and will trigger compliance violations:**

- ❌ Missing `runAsNonRoot: true`
- ❌ Missing `runAsGroup` configuration
- ❌ Missing `seccompProfile` settings
- ❌ Missing `allowPrivilegeEscalation: false`
- ❌ Missing `readOnlyRootFilesystem: true`

**This is intentional for testing the AI compliance workflow!**

## 🤖 AI Compliance Workflow

This repository is designed to be used with the AI-enabled compliance workflow:

1. **Trigger Compliance Check**: The AI workflow will scan this deployment
2. **Detect Violations**: Security context violations will be identified
3. **Auto-Remediation**: AI will generate fixes based on `source_of_truth.yaml`
4. **Create PR**: Automated pull request with security improvements

## 🔄 Continuous Integration

This repository integrates with:
- **GitHub Actions** for CI/CD
- **n8n Workflows** for compliance automation
- **ArgoCD** for GitOps deployment