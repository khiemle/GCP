
## Group of services from GCP
![alt text](./images/whole-services.png)

## Compare storage option

![alt text](./images/compare-storage-option-1.png)

![alt text](./images/compare-storage-option-2.png)

## Notes
IaaS Infastructure as services
* Compute Engine

SaaS Software as services

PaaS Platform as services: 
* App Engine

Hybrid: 
* Kubernetes Engine

## `sed` command
```
sed -i -e 's/PROJECT_ID/'$DEVSHELL_PROJECT_ID/ mydeploy.yaml
sed -i -e 's/ZONE/'$MY_ZONE/ mydeploy.yaml
```

## Creates an artificial CPU load 

It forces the CPU to continuous attempt to compress random data
```
dd if=/dev/urandom | gzip -9 >> /dev/null &
```

## IAM concepts

- Permissions are represented with the following syntax
<service>.<resource>.<verb>


## Useful commands
Copy file to instance
```
gcloud compute scp <file> <instance name>:~\...
```
Rename multi files
```
find . -type f -name 'notes.md' -execdir mv {} readme.md \;
```



