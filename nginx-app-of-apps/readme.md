## app of apps example

This is the root directory of an example for the app of apps pattern. It also features a post-sync job, which is
intentionally *not* part of the helm-package being deployed.

It consists of the following apps:
* The parent app defined by `app/nginx-helm-directory.yaml`. That's not entirely true.
* The app defined by the helm-chart referenced by the above app. 


