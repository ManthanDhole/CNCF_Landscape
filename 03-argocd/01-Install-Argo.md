# ArgoCD
A declarative GitOps Continuous Delivery Tool for Kubernetes

## Install ArgoCD

#### 1. Add ArgoCD Repository & Install the Chart in the Cluster
```
helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
helm search repo

helm install argocd argo/argo-cd 
helm install argocd argo/argo-cd -n argocd --create-namespace
helm install argocd argo/argo-cd --version 10.8.4 -n argocd --create-namespace

helm list -A    ## List all the installed releases in all namespaces
```

#### 2. Verify ArgoCD is installed
```
kubectl get ns
kubectl get all -n argo
```

#### 3. Accessing UI
In order to access the server UI you have the following options:
```
kubectl port-forward service/argocd-server -n argocd 8080:443
```
and then open the browser on http://localhost:8080 and accept the certificate

Login credentials
UserName: admin
Password: Use following command to get the password
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

#### 4. Uninstall Argo App, Delete CRDs & Delete Argo Namespace
```
helm uninstall argocd -n argo

kubectl get crd
kubectl delete crd applications.argoproj.io applicationsets.argoproj.io appprojects.argoproj.io

kubectl delete namespace argo
```