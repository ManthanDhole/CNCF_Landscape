# Kyverno

#### 1. Installation

```
helm repo add kyverno https://kyverno.github.io/kyverno/
helm repo update
helm install kyverno kyverno/kyverno -n kyverno --create-namespace
```

To View a UI Dashboard for Policies
```
helm repo add policy-reporter https://kyverno.github.io/policy-reporter
helm repo update

# Install Policy Reporter with UI and Kyverno plugin enabled

helm install policy-reporter policy-reporter/policy-reporter \
  --namespace policy-reporter \
  --create-namespace \
  --set ui.enabled=true \
  --set plugin.kyverno.enabled=true

kubectl get all -n policy-reporter
kubectl port-forward service/policy-reporter-ui 8080:8080 -n policy-reporter
```