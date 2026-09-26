# Run Sample Applications in Kind Cluster: Nginx & Sonarqube 

```
kubectl run nginx --image=nginx:latest
kubectl expose pod nginx --port=8000 --target-port=80 --type=NodePort --name=nginx-svc

kubectl port-forward service/nginx-svc 8500:8000

kubectl run sonarqube --image=sonarqube:latest
kubectl expose pod sonarqube --port=9500 --target-port=9000 --type=NodePort --name=sonarqube-svc

kubectl port-forward service/sonarqube-svc 9500:9500
```

#### Create Deployment and scale Replicas 

```
kubectl create deployment nginx-deploy --image=nginx:latest

kubectl scale deployment nginx-deployment --replicas=5  ## Create 5 Replicas of Nginx Pod
kubectl scale deployment nginx-deployment --replicas=50 

kubectl get pods -o wide
kubectl get pods -o wide --sort-by='.spec.nodeName'     ## Sort Pods by Node Name
```