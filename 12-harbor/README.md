# Harbor: Container Registry

An open source trusted cloud native registry project that stores, signs, and scans content

#### 1. Install Harbor using Helm

```
helm repo add harbor https://helm.goharbor.io
helm repo update
helm fetch harbor/harbor --untar

helm install my-harbor harbor/ -n harbor --create-namespace

kubectl get all -n harbor
kubectl get pvc -n harbor
kubectl get pods -n harbor
```

#### 2. Accessing Harbor Dashboard

Using a NodePort to view Harbor UI Dashboard
```
helm upgrade my-harbor harbor/harbor \
  --namespace harbor \
  --reuse-values \
  --set expose.type=nodePort \
  --set expose.tls.enabled=false \
  --set externalURL=http://localhost:30002

kubectl rollout status deployment/my-harbor-core -n harbor
```

```
## Getting Admin Password
kubectl get secrets -n harbor

kubectl describe secret my-harbor-core -n harbor

kubectl get secret
kubectl get secret my-harbor-core -n harbor -o jsonpath='{.data.HARBOR_ADMIN_PASSWORD}' | base64 -d

kubectl port-forward svc/harbor 9000:80 -n harbor
```
[Local Harbor UI](http://localhost:9000)
UserName: admin
Password: Harbor12345

