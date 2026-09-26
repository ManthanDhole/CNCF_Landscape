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
kubectl cluster-info --context test-cluster     ## 
```

Multi Node Cluster
```
kind create cluster --config multi-node-cluster.yaml

kubectl config current-context
kubectl get nodes
```

#### 3. Kind Commands

```
kind get clusters   ## View what clusters are available
kind get nodes      ## View which nodes are associated with the kind (default) cluster
kind get nodes --name test-cluster      ## View which nodes are associated with the test-cluster
```

```
kind delete cluster --name test-cluster     ## Delete cluster
```