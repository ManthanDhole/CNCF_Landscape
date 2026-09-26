# Run Sample Applications in Kind Cluster: Nginx & Sonarqube 

```
kubectl run nginx --image=nginx:latest
kubectl expose pod nginx --port=8000 --target-port=80 --type=NodePort --name=nginx-svc

kubectl port-forward service/nginx-svc 8500:8000

kubectl run sonarqube --image=sonarqube:latest
kubectl expose pod sonarqube --port=9500 --target-port=9000 --type=NodePort --name=sonarqube-svc

kubectl port-forward service/sonarqube-svc 9500:9500
```