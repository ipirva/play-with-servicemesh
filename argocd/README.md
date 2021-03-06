Argocd version is [**v2.1.7**](https://github.com/argoproj/argo-cd/releases)

[Argocd Getting Started](https://argo-cd.readthedocs.io/en/stable/getting_started/)

After the installation the dashboard username is admin and the password can be grabbed from:
```kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d```

It is very useful to install the Argocd CLI. With brew this goes as:
```brew install argocd```

Once Argocd installed, I use the CLI to create the different apps and then bring all of them into sync from the Argocd UI.

Some useful argocd CLI commands:

```argocd login argocd.play.p2o.be
argocd cluster add $(kubectl config current-context)

argocd app create argocd --repo https://github.com/ipirva/play-with-servicemesh --path argocd/overlay/production --dest-server https://dev-cluster-1-apiserver-1952821174.eu-west-3.elb.amazonaws.com:6443

argocd app create tekton --repo https://github.com/ipirva/play-with-servicemesh --path tekton/overlay/production --dest-server https://dev-cluster-1-apiserver-1952821174.eu-west-3.elb.amazonaws.com:6443

argocd app create external-dns --repo https://github.com/ipirva/play-with-servicemesh --path external-dns/overlay/production --dest-server https://dev-cluster-1-apiserver-1952821174.eu-west-3.elb.amazonaws.com:6443

argocd app create hipstershop --repo https://github.com/ipirva/microservices-demo --path online-boutique/kubernetes-manifests/overlay/production --dest-server https://dev-cluster-1-apiserver-1952821174.eu-west-3.elb.amazonaws.com:6443
argocd app list
argocd app sync hipstershop
```
