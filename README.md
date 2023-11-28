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

Or if you're installing it on EKS or some other platform, you have to patch 
service file:

```bash
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

After patching it, you can get the IP address using:

```bash
kubectl -n argocd get svc
```
and check for external IP.

### Password and login from CLI

```bash
argocd login --username admin --password $(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d) --insecure localhost:8080

# Only password

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```
