build it

```
helm package . -d ../../helm-repo
```

update the repo index
```
helm repo index ../../helm-repo --url http://192.168.65.254:8123
```

