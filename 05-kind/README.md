# Kind - Kubernetes IN Docker

#### 1. Install Kind CLI 
```
choco install kind      
kind --version
```

#### 2. Create a cluster using Kind
Single Node Cluster
```
kind create cluster --name test-cluster

kubectl config current-context      ## Shows which cluster are we connected via kubectl  
kubectl get nodes                   ## Show how many nodes are created    
kubectl cluster-info --context test-cluster     ## 
```

Multi Node Cluster
```
kind create cluster --config multi-node-cluster.yaml

kubectl config current-context
kubectl get nodes
```
