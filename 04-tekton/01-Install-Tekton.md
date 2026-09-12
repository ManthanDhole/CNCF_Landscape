# Tekton

#### Install Tekton 
[Official Tekton Page](https://tekton.dev/docs/installation/)

```
## Tekton Pipelines
kubectl apply --filename https://infra.tekton.dev/tekton-releases/pipeline/latest/release.yaml

## Tekton Dashboard
kubectl apply --filename https://infra.tekton.dev/tekton-releases/dashboard/latest/release.yaml

## Tekton Operator (Optional)
kubectl apply -f https://infra.tekton.dev/tekton-releases/operator/previous/v0.81.1/release.yaml
```
 
#### Access the Tekton Web UI
There are 2 ways to access Tekton Dashboard UI 

1. Using Kubectl Proxy
```
kubectl proxy
```

2. Using PortForward
```
kubectl port-forward service/tekton-dashboard 9097:9097 -n tekton-pipelines
```
[Localhost Tekton Dashboard](http://localhost:9097)

#### Install Tekton CLI

```
choco install tektoncd-cli --confirm    ## Windows
brew install tektoncd-cli               ## MacOS
sudo apt install -y tektoncd-cli        ## Linux  
```

Verify Tekton CLI
```
tkn version
```

#### Common Tekton Commands

```
tkn task list -A        ## List all tekton tasks from All Namespaces
tkn task list -n test   ## List tekton tasks from Test Namespace

tkn pipeline list -n test
tkn pipelinerun list -n test
```

Manually trigger taskrun & pipelinerun using tkn cli
```
tkn task start hello-task -n test
tkn pipeline start hello-pipeline -n test
```