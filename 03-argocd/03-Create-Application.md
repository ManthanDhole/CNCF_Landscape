# Creating Application in Argo

1. Create an Application which sync's deployments/services from GitHub Repository
```
Navigate to Argo Applications > New App > 
Application Name (nginx) > Project Name (default) > Sync Policy (Automatic) > 

Source > Repository URL (select kubernetes-resources from the drop down menu) >
Revision (Head) > Path (nginx-app) [FolderName containing manifests that you want to deploy] >


Destination > Cluster URL (https://kubernetes.default.svc) >
Namespace (nginx) > Create
```