To create an Argo CD Application for Grafana, you'll reference the official Grafana Helm chart repository (or a custom one if needed). For the official Grafana Helm chart, add the repository to Argo CD:

```sh
argocd repo add https://prometheus-community.github.io/helm-charts
```

Then, create the Argo CD Application with the Grafana Helm chart, pointing to your Git repository and the Grafana folder:

```sh
argocd app create grafana \
  --repo https://github.com/your-org/your-gitops-repo.git \
  --path infrastructure/monitoring/grafana \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace monitoring \
  --helm-chart prometheus-community/grafana \
  --helm-set-file values=values.yaml \
  --sync-policy automated
```