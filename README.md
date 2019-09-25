# Installing Helm
* `kubectl create serviceaccount --namespace kube-system tiller`
* `kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller`
* `kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'`
* `helm init --service-account tiller --upgrade`

# Installing Flux
* `helm repo add fluxcd https://charts.fluxcd.io`
* `helm upgrade -i flux --set helmOperator.create=true --set helmOperator.createCRD=false --set git.url=git@github.com:MikaelElkiaer/flux-get-started --set git.pollInterval=1m --set syncGarbageCollection.dry=true --namespace flux fluxcd/flux`

# Installing Kubeseal
* `wget https://github.com/bitnami-labs/sealed-secrets/releases/download/v0.9.0/kubeseal-linux-amd64 -O kubeseal`
* `sudo install -m 755 kubeseal /usr/local/bin/kubeseal`
