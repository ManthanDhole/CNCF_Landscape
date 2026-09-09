# Cluster Provisioning

### Local Cluster setup using KIND
#### 1. Install Docker, Kind, Kubectl 
[Docker Installation](https://docs.docker.com/desktop/setup/install/windows-install/)
```
choco install kind
choco install kubernetes-cli

kind --version
kubectl version
```

#### 2. Provision cluster using the following docker desktop or kind 

Docker Desktop
```
1. Settings > Resources > Resource Allocation
CPU Limit - 12
Memory Limit - 8 GB
Disk Usage Limit - 250 GB

2. Kubernetes > Cluster Setting > Select Kind > 2 or 3 Nodes > Create Cluster
```

Kind
```
kind create cluster --name cncf-cluster
```

#### 3. Verify the cluster is running and kubectl can communicate with the cluster
```
kubectl config get-contexts
kubectl config current-context
```

#### 4. To switch from one cluster to another use the following command 
```
kubectl config use-context docker-desktop
kubectl config use-context cncf-cluster
```

#### 5. Verify is you can see the resources inside the cluster using following command
```
kubectl get namespaces
kubectl get pods 
kubectl get pods -n kube-system 
```