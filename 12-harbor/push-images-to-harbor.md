# Push Images to Harbor Registry

```
docker pull nginx:stable-trixie

docker tag nginx:stable-trixie localhost:30002/demo-images/nginx:stable-trixie

docker push localhost:30002/demo-images/nginx:stable-trixie     ## This wont work
```

#### Edit local Docker Configuration File & Add local Harbor address to the insecure-registries list

Navigate to Docker Desktop > Settings > Docker Engine > Edit the Configuration file
```
{
  "builder": {
    "gc": {
      "defaultKeepStorage": "20GB",
      "enabled": true
    }
  },
  "experimental": false,
  "insecure-registries": ["harbor.local.domain:port"]   ## Example File Syntax
  "insecure-registries": ["localhost:30002"]            ## Actual Domain hosted locally
}
```
After editing the configuration > Click Apply & Restart

```
kubectl port-forward svc/my-harbor-core 30002:80 -n harbor

docker login localhost:30002

```