## get types of resources
```
gcloud deployment-manager types list
gcloud deployment-manager types list | grep instance
```
## get zones
```
gcloud compute zones list
```
## get machine types
```
gcloud compute machine-types list
```
## get machine types selfLink
```
gcloud compute machine-types describe f1-micro --zone us-central1-a | grep selfLink
```

## get images list
```
gcloud compute images list
gcloud compute images list | grep debian
```

## get image selfLink
```
gcloud compute images describe debian-9-stretch-vxxxx --project debian-cloud | grep selfLink
```

## get networks list from VPC
```
gcloud compute networks list
```

## get selfLink of network from VPC
```
gcloud compute networks describe default | grep selfLink
```

## Create new deployment
```
gcloud deployment-manager deployments create my-first-depl --config mydeploy.yaml
```

## Update deployment
```
gcloud deployment-manager deployments update my-first-depl --config mydeploy.yaml
```








