# Teleport 

#### 1. Create Certificates
```
openssl genrsa -out teleport.key 2048

openssl req -x509 -nodes -days 365 -new -key teleport.key -out teleport.crt -subj "/CN=localhost"
```


#### 2. Installation

```
helm repo add teleport https://charts.releases.teleport.dev
helm repo update
```

Create a Secret having TLS Certificate
```
kubectl create namespace teleport-cluster

kubectl create secret tls local-teleport-certs --cert=teleport.crt --key=teleport.key -n teleport-cluster
```

Install Teleport & Access Web UI
```
helm install teleport-cluster teleport/teleport-cluster \              
--namespace teleport-cluster \
-f teleport-cluster-values.yaml

kubectl port-forward -n teleport-cluster service/teleport-cluster 8443:443
```

Create an Admin User to log into Teleport UI
```
kubectl exec -i -n teleport-cluster deploy/teleport-cluster-auth -- tctl users add teleport-admin --roles=editor,access
```

