
## Concepts
- Reliable
- Repeatable

==> Deployments

- Infastructure as code

## CI

### Code --> new feature branch `trigger`

- Source repositories (or Github, Bitbucket)
- Builder Trigger (Container Registry)
- Trigger on branch or tag
- cloud build file configurations
    * json
    * yaml

### Build --> Store 

- Constainer Builder: Build (or Jenkins, CircleCI)
    * Help to set up building pipeline
    * The result is docker image, to make sure the application can work the same
    * Auto push to Constainer Registry

- Docker image
    * Example
    ```
    FROM gcr.io/google_appengine/nodejs
    COPY app.ss /app/
    RUN echo "This run during the build process..."
    CMD node app.js
    ```
    ```
    docker build -t <docker image name> .
    docker images
    docker run -d -p 8080:8080 <docker image name>
    docker ps
    docker stop <id>
    
    ```
    * Build images with docker
    ```
    docker tag <docker image name> gcr.io/<GCP project id>/<docker image name>
    // Push the local docker image to Container Registry
    gcloud docker -- push gcr.io/<GCP project id>/<docker image name>
    ```
    * Build images with gcloud tool
    ```
    // Container build in the local folder
    gcloud container builds submit -t gcr.io/<GCP project id>/<docker image name 2> .
    ```
- Container Engine - Kubernetes  Engine
    * Container cluster
    * Create the deployment with image, expose the port of container
    ```
    kubectl run <deployment name> --image=gcr.io/<GCP project id>/<docker image name> --port=8080
    ```
    * Create Services (LoadBalancer) target to container opened port
    ```
    kubectl expose devployment <deployment name> --type=LoadBalancer --port=80 --target-port=8080
    ```
    * Scale 
    ```
    kubectl scale deployment <deployment name> --replicas=3
    ```


- Container Registry: Images 
    * Support Pub/Sub: publishes build status

### Deploy (Development)
- Take the images and launch VM
- Deployment manager (or Teraform, Chef, Ansible...)
    * Launch another GCP resources
    * Define template properties, environment variables
    * Start up script for VM
    * ...
    * Jinja or Python code --> generate the Yaml configurations
    * Can reuse template deployment with diference environment, variables
        * ip 
        * persitent disk
        * start up script of VM
- Deployment Manager practice
    - create infastructure, infastructure as code
    ```
    gcloud deployment-manager deployments create <deployment name> --config <yaml file>
    ```
    - delete the deployment
    ```
    gcloud deployment-manager deployments delete <deployment name> 
    ```
    - with python code, can define the variables, properties inside the yaml file and use them in python code

    

### Test


## CD

### Code --> new release branch `trigger`

### Build --> Store

### Deploy (Stagging)

### Test --> approval will trigger to release step

### Release (Production)
- Canary
- Blue-green deployments

### Monitor
- Stackdriver






