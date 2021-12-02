https://argo-cd.readthedocs.io/en/stable/getting_started/

argocd-server username is admin and password:
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

brew install argocd

argocd login argocd.play.p2o.be
argocd cluster add $(kubectl config current-context)

argocd app create argocd --repo https://github.com/ipirva/play-with-servicemesh --path argocd/overlay/production --dest-server https://dev-cluster-1-apiserver-1952821174.eu-west-3.elb.amazonaws.com:6443

argocd app create tekton --repo https://github.com/ipirva/play-with-servicemesh --path tekton/overlay/production --dest-server https://dev-cluster-1-apiserver-1952821174.eu-west-3.elb.amazonaws.com:6443

argocd app create hipstershopshop --repo https://github.com/ipirva/microservices-demo --path deployment/kubernetes-manifests --dest-server https://dev-cluster-1-apiserver-1952821174.eu-west-3.elb.amazonaws.com:6443
argocd app list
argocd app sync hipstershop
