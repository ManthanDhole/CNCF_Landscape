# ArgoCD

#### Install ArgoCD
1. Add ArgoCD Repository & Install the Chart in the Cluster
```
helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
helm search repo

helm install argocd argo/argo-cd 
helm install argocd argo/argo-cd argocd --create-namespace
helm install argocd argo/argo-cd --version 10.8.4
```

2. Verify ArgoCD is installed
```
kubectl get ns
kubectl get all -n argo
```