# argo apps

This directory contains app manifests for argocd.

Deploy them using kubectl, and argocd will pick them up:

```
kubectl apply -f <app-name>.yaml
```

to get rid of it again:

```
kubectl delete -f <app-name>.yaml
```

## selfhealing nginx

let argocd deploy it:

```
kubectl apply -f selfhealing-nginx.yaml
```

scale up the number of pods

```
kubectl -n firstns scale deployment/nginx --replicas=4
```

Watch argo getting rid of the newly appeared pods. Note that this also happens when `prune: false`. No pruning
is happening here yet. However, the replicaset which we manually set to 4 instances gets reverted back to how it's
defined in git (2 resources). As a consequence, the newly created pods disappear.

## nginx-helm-directory

This is a bit different. Point argocd to `argo-apps/nginx-helm-directory` and argo will deploy whatever is in there.
This happens to be an argocd app manifest, which in turn points to a helm-chart, which then gets deployed.
This results in two applications that are managed by argocd:

* The app defined by `argo-apps/nginx-helm-directory/nginx-helm-directory.yaml`. That's probably an app of apps.
* The app defined by the helm-chart referenced by the above app.



