## Create a Cluster
```
gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2
```
## Get credentials from a Cluster

## Run a pod with image
```
kubectl run nginx --image=nginx:1.0.0
```
## Expose the pod with port
```
kubectl expose nginx --port 80 type LoadBalancer
```
## Create Deployments
### With YAML file
```
```

## Scale deployments
```
kubectl scale deployment nginx --replicas 3
```

## Get information 

Add `--watch` to check status

```
* kubectl get nodes
* kubectl get pods
* kubectl get deployments
* kubectl get services
* kubectl describe <exactl_name>
```

## Checking the kubectl context
```
kubectl config get-contexts
kubectl config use-context docker-for-desktop
```