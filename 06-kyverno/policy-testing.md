# Policy Testing

1. [Prevent Latest Image Tags](./policies/prevent-latest-image-tag.yaml)
```
kubectl apply -f ./policies/prevent-latest-image-tag.yaml

kubectl run  nginx --image=nginx:latest
```

```
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
    name: nginx-pod
spec:
    containers:
        - name: latest-nginx-image
          image: nginx:latest
EOF
```

2. [Image Tag should not be Empty](./policies/image-tag-should-not-be-empty.yaml)
```
kubectl apply -f ./policies/image-tag-should-not-be-empty.yaml

kubectl run  nginx --image=nginx
```

```
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
    name: nginx-pod
spec:
    containers:
        - name: nginx-image-without-tag
          image: nginx
EOF
```

3. [Prevent Exec into Pods](./policies/prevent-exec-into-containers.yaml)
```
kubectl apply -f ./policies/prevent-exec-into-containers.yaml

kubectl run  nginx --image=nginx:1.31.8
kubectl exec -it nginx -- sh
```

4. [Include Environment Label in Metadata](./policies/include-environment-label-in-metadata.yaml)
```
kubectl apply -f ./policies/include-environment-label-in-metadata.yaml

kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
    name: nginx-pod
spec:
    containers:
        - name: nginx-without-env-label
          image: nginx:1.31.0
EOF
______________Fixed Below________________________

kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
    name: nginx-pod
    labels:
        environment: dev
spec:
    containers:
        - name: nginx-without-env-label
          image: nginx:1.31.0
EOF
```

5. [Creating Exceptions](./exceptions/exec-into-namespaced-pods.yaml)
You'll need to enable the Kyverno's Policy Exception Feature before any of your exceptions applied and used. If you proceed without enabling this flag, then the expection will live in the cluster, but would not have any effect

```
helm upgrade kyverno kyverno/kyverno \
  --namespace kyverno \
  --set features.policyExceptions.enabled=true \
  --set features.policyExceptions.namespace=kyverno

kubectl apply -f ./exceptions/exec-into-namespaced-pods.yaml
kubectl get policyexceptions.policies.kyverno.io -n kyverno

_________________________________________
kubectl create namespace allow-exec-to-nginx

kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
    name: nginx-pod
    namespace: allow-exec-to-nginx
    labels:
        environment: dev
spec:
    containers:
        - name: nginx-without-env-label
          image: nginx:1.31.0
EOF

kubectl exec -it nginx-pod -n allow-exec-to-nginx
_________________________________________
kubectl create namespace exempted-namespace

kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
    name: nginx-pod
    namespace: exempted-namespace
    labels:
        environment: dev
spec:
    containers:
        - name: nginx-without-env-label
          image: nginx:1.31.0
EOF

kubectl exec -it nginx-pod -n exempted-namespace
```
