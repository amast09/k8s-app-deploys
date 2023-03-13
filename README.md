# k8s-app-deploys

Required for local mac ingress

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.41.2/deploy/static/provider/cloud/deploy.yaml

kubectl port-forward --namespace=ingress-nginx service/ingress-nginx-controller 80:80
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