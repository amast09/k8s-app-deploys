# k8s-app-deploys

Required for local mac ingress

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.41.2/deploy/static/provider/cloud/deploy.yaml

kubectl port-forward --namespace=ingress-nginx service/ingress-nginx-controller 80:80
```

Create Kind Cluster

```
kind create cluster --name k8s-app-deploys --config clusters/local/kind-cluster.yaml
export GITHUB_TOKEN=???
export GITHUB_USER=???
flux bootstrap github \
  --owner=amast09 \
  --repository=k8s-app-deploys \
  --branch=main \
  --personal \
  --private=false \
  --read-write-key=true \
  --reconcile=true \
  --path=clusters/local
```

Tear Down Cluster

```
kind delete cluster --name k8s-app-deploys
```

Quick testing

```
kubectl delete ingress local-ingress
kubectl delete service pr
kubectl delete deployment pr

kubectl create -f k8s/service.yml
kubectl create -f k8s/deployment.yml
kubectl create -f k8s/local-ingress.yml
```
