# OPA - Gatekeeper

#### Install OPA 
```
helm repo add gatekeeper https://open-policy-agent.github.io/gatekeeper/charts
helm repo update

helm install gatekeeper gatekeeper/gatekeeper \
  --namespace gatekeeper-system \
  --create-namespace

## Install GateKeeper Policy Manager Dashboard

helm upgrade --install --namespace gatekeeper-system \
    --set image.tag=v2.1.2 --values my-values.yaml \
    gatekeeper-policy-manager oci://quay.io/sighup/charts/gatekeeper-policy-manager \
    --version 0.20.2
```

To view the OPA Dashboard, use Port Forward
```
export POD_NAME=$(kubectl get pods --namespace gatekeeper-system -l "app.kubernetes.io/name=gatekeeper-policy-manager,app.kubernetes.io/instance=gatekeeper-policy-manager" -o jsonpath="{.items[0].metadata.name}")

export CONTAINER_PORT=$(kubectl get pod --namespace gatekeeper-system $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")

echo "Visit http://127.0.0.1:8080 to use your application"

kubectl --namespace gatekeeper-system port-forward $POD_NAME 8080:$CONTAINER_PORT
```

#### Install Constraint CRD and the constraint
##### 1. Disallow Latest tag for Images 
```
kubectl apply -f ./disallow-latest-image-tag/constraint-template.yaml
kubectl get crd

kubectl apply -f ./disallow-latest-image-tag/disallow-latest-tag-constraint.yaml

kubectl run nginx --image=nginx:latest
kubectl run nginx --image=nginx:1.31.1
```

##### 2. Prevent Exec into Containers
```
kubectl apply -f ./block-exec-into-containers/constraint-template.yaml
kubectl get crd
kubectl apply -f ./block-exec-into-containers/blockexec-constraint.yaml

kubectl exec -it nginx -- sh
```