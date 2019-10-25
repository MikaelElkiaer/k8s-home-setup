# Installing Helm
* `kubectl create serviceaccount --namespace kube-system tiller`
* `kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller`
* (GKE) `kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'`
* `helm init --service-account tiller --upgrade`

# Installing Flux
## Install fluxctl
* `wget https://github.com/fluxcd/flux/releases/download/1.15.0/fluxctl_linux_amd64 -O fluxctl`
* `sudo install -m 755 fluxctl ~/bin/fluxctl`
## Install controllers
* `helm repo add fluxcd https://charts.fluxcd.io`
* `helm upgrade -i flux --set helmOperator.create=true --set helmOperator.createCRD=false --set git.url=git@github.com:MikaelElkiaer/flux-get-started --set git.pollInterval=1m --set syncGarbageCollection.enabled=true --namespace flux fluxcd/flux`

Once started, call

* `fluxctl identity --k8s-fwd-ns flux`

in order to get the public SSH key to add to the GitHub repository as a Deploy Key.

# Installing Kubeseal
* `wget https://github.com/bitnami-labs/sealed-secrets/releases/download/v0.9.0/kubeseal-linux-amd64 -O kubeseal`
* `sudo install -m 755 kubeseal ~/bin/kubeseal`

# Installing drone (CLI)
* `curl -L https://github.com/drone/drone-cli/releases/download/v1.1.0/drone_linux_amd64.tar.gz | tar zx`
* `sudo install -t ~/bin drone`
