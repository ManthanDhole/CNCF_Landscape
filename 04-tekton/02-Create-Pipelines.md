# Tekton Concepts

Task > TaskRun 
Pipeline > PipelineRun

#### Create Tasks & TaskRuns

[First Task](./yaml-files/task-1/task.yaml)
[First TaskRun](./yaml-files/task-1/taskrun.yaml)

```
kubectl create namespace test

kubectl apply -f ./yaml-files/task-1/task.yaml
kubectl apply -f ./yaml-files/task-1/taskrun.yaml

kubectl get task -n test
kubectl get taskRun -n test

```

[Second Task](./yaml-files/task-2/task-2.yaml)
[Second TaskRun](./yaml-files/task-2/taskrun-2.yaml)

```
kubectl apply -f ./yaml-files/task-2/task-2.yaml
kubectl apply -f ./yaml-files/task-2/taskrun-2.yaml

kubectl get task -n test
kubectl get taskRun -n test
```

#### Create Pipeline & PipelineRun

[Pipeline](./yaml-files/pipeline/pipeline.yaml)
[PipelineRun](./yaml-files/pipeline/pipelinerun.yaml)

```
kubectl apply -f ./yaml-files/pipeline/pipeline.yaml
kubectl apply -f ./yaml-files/pipeline/pipelinerun.yaml

kubectl get pipeline -n test
kubectl get pipelinerun -n test
```
