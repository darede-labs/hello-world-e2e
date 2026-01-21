# hello-world-e2e - GitOps Repository

This repository contains the Kubernetes manifests for the `hello-world-e2e` application.

## 📁 Repository Structure

```
hello-world-e2e/
├── manifests/             # Kubernetes manifests
│   ├── deployment.yaml    # Deployment configuration
│   ├── service.yaml       # Service configuration
│   └── ingress.yaml       # Ingress configuration
├── argocd-application.yaml # ArgoCD Application manifest
└── README.md              # This file
```

## 🚀 Deployment

This application is deployed using **GitOps** with **ArgoCD**.

### Initial Deployment

Apply the ArgoCD Application manifest to your cluster:

```bash
kubectl apply -f argocd-application.yaml
```

ArgoCD will automatically sync the manifests from this repository to your cluster.

### Updating the Application

To update the application:

1. Modify the manifests in the `manifests/` directory
2. Commit and push your changes:
   ```bash
   git add manifests/
   git commit -m "feat: update deployment configuration"
   git push origin main
   ```
3. ArgoCD will automatically detect the changes and sync them to the cluster

### Manual Sync

If you need to manually sync the application:

```bash
argocd app sync hello-world-e2e
```

## 🔍 Monitoring

- **Application URL**: https://hello-world-e2e.timedevops.click
- **Health Endpoint**: https://hello-world-e2e.timedevops.click/health
- **Readiness Endpoint**: https://hello-world-e2e.timedevops.click/ready
- **Metrics Endpoint**: https://hello-world-e2e.timedevops.click/metrics

## 📊 Observability

### Logs (Loki)

View logs in Grafana:
```
{namespace="default", app_kubernetes_io_name="hello-world-e2e"}
```

### Metrics (Prometheus)

Metrics are automatically scraped by Prometheus if the pod has the annotation:
```yaml
prometheus.io/scrape: "true"
prometheus.io/port: "3000"
prometheus.io/path: "/metrics"
```

### Dashboards (Grafana)

- Service Overview: `https://grafana.timedevops.click/d/service-overview?var-namespace=default&var-app=hello-world-e2e`

## 🔐 Security

- All images should be scanned before deployment
- Secrets should be managed via External Secrets or Sealed Secrets
- RBAC policies should follow the principle of least privilege

## 🛠️ Troubleshooting

### Check Pod Status
```bash
kubectl get pods -n default -l app.kubernetes.io/name=hello-world-e2e
```

### Check Logs
```bash
kubectl logs -n default -l app.kubernetes.io/name=hello-world-e2e --tail=100
```

### Check ArgoCD Sync Status
```bash
argocd app get hello-world-e2e
```

### Force Sync
```bash
argocd app sync hello-world-e2e --force
```

## 📝 Notes

- This repository follows GitOps best practices
- All changes should be made through pull requests
- CI/CD pipelines should update the `image` field in `deployment.yaml` automatically

## 🔗 Links

- **GitHub Org**: https://github.com/darede-labs
- **Application Repo**: (Link to application source code repository)
- **ArgoCD UI**: https://argocd.timedevops.click
- **Grafana**: https://grafana.timedevops.click

---

**Managed by**: Platform Team
**GitOps Tool**: ArgoCD
**Last Updated**: 2026-01-21
