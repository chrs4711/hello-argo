# hello argo
Example project to play around with argocd.

Prerequisites:
* minikube is intalled
* the argocd cli application is installed

## Local setup

Start minikube:
```
minikube start
```

Create namespace where ArgoCD will live in:
```
kubectl create namespace argocd
```

Install argocd
```
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Look at all the things now in the namespace:
```
kubectl get -n argocd all
```

Check the port that is exposed by the argocd-server service (usually 80)
```
kubectl get -n argocd svc/argocd-server
```

Start a port forward to access the admin ui:
```
kubectl port-forward -n argocd svc/argocd-server 8888:80
```

Fetch the initial password for user `admin`:
```
argocd admin initial-password -n argocd
```

### Ingress

put into `/etc/hosts`:

```
127.0.0.1       nginx.local
```






