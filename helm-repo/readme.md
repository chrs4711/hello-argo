# helm repo to play around with

Create a directory `helm-repo` and `cd` into it. Then serve it!

e.g. with docker:
```
docker run --rm -v $(pwd):/usr/share/nginx/html:ro -p 8123:80 nginx
```

or with python:
```
python3 -m http.server 8123
```

Throw a packaged chart into this folder:
```
cp mychart.tgz helm-repo
```

Then `cd` into the repo and (re-)create the repo index:
```
helm repo index . --url http://<address>:8123
```

Make sure that `<address>` points to something that clients can actually reach.

Make this repo known to helm:
```
helm repo add my-repo http://<address>:8123
helm repo update
```

### Use with Argo CD

Assuming Argo CD is running within minikube, we might be able to connect to the host using `host.minikube.internal`.
If that doesn't work, we can find the IP-Address:

Go into minikubes VM:
```
minikube ssh
```

Find the IP in `/etc/hosts`:
```
grep "host.minikube" /etc/hosts
```

Make this repo known to Argo CD by connecting a new repository:
* Settings
* Repositories
* Connect Repo
* Via HTTPS
* Enter repository url with http!, e.g. `http://192.168.23.5:8123`
