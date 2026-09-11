# Helm - Package Manager of k8s applications
Helm is a tool that streamlines installing and managing Kubernetes applications.

### Charts
Charts are Helm Packages that contain at least 2 things:
1. A description of the package - Chart.yaml
2. One or more templates, which contain Kubernetes Manifest files

#### Install Helm 
```
### Open Powershell in Administrator Mode
choco install kubernetes-helm

### Verify if the Helm Cli is installed
helm version
```

#### Helm Commands
1. List installed helm charts
```
helm list
```

2. Find Charts to install on [Artifact Hub](https://artifacthub.io/packages/search?kind=0)
```
helm search hub     ### List all available charts in artifact hub
helm search hub argo    ### List all available charts related to argo

helm search repo    ### List repositories added to local helm client (with helm repo add)
helm repo add <app-name>    ### Added a repo to local helm client that can be installed in the cluster
```

3. Add a Repository & Install a Chart in the Cluster
```
helm repo add <chart-name> <repository-url>

helm repo add jenkins https://charts.jenkins.io
helm repo update

helm search repo

helm install my-jenkins jenkins/jenkins    ### installs jenkins resources in default namespace
helm install my-jenkins jenkins/jenkins --namespace jenkins --create-namespace

helm install my-jenkins jenkins/jenkins --version 5.9.56
```

4. Verify the installed resources using kubectl commands in the cluster
```
helm list -A  ### check the installed charts in the cluster in all namespaces

kubectl get ns
kubectl get all -n jenkins
kubectl get pods -n jenkins --watch
```

5. Access the UI using port-forward to localhost
```
kubectl exec --namespace jenkins -it svc/my-jenkins -c jenkins -- cat run/secrets/additional/chart-admin-password && echo  ## Windows
kubectl exec --namespace jenkins -it svc/my-jenkins -c jenkins -- /bin/cat /run/secrets/additional/chart-admin-password && echo  ## Mac & Linux

kubectl --namespace jenkins port-forward svc/my-jenkins 8080:8080
```
Create a sample Pipeline and Run it
```
node {
    stage("example") {
        sh 'ls'
        sh 'pwd'
        sh 'whoami'
    }
}
```


6. Uninstall a release from the cluster
```
helm list 
helm uninstall <release-name>
helm uninstall my-jenkins
helm uninstall my-jenkins -n jenkins
```

6. Delete if any CRD are still available in the cluster
```
kubectl get crd
kubectl delete crd <crd-name>
```