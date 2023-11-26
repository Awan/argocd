# Learn Argocd

### How to install?

```bash
helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
kubectl create ns argocd
helm install argocd argo/argo-cd -n argocd
kubectl port-forward service/argocd-server -n argocd 8080:443
```

Now you can access argocd on https://localhost:8080

### Password and login from CLI

```bash
argocd login --username admin --password $(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d) --insecure localhost:8080

# Only password

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```
