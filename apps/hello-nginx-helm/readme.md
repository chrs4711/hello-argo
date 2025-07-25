# nginx example app

Created as a helm chart.

## Direct usage with ArgoCD

It's possible to create an app in ArgoCD and point to this directory as a source.

Is it also possible to create an ArgoCD app xml manifest, which in turn points to this directory?

## Create a package and put it in a repository

build it:
```
helm package . -d ../../helm-repo
```

update the repo index
```
helm repo index ../../helm-repo --url http://192.168.65.254:8123
```

