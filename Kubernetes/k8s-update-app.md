An experiment of the project is to modify the message of the Python application from "Hello World" to "Hello Luxembourg" and see the minimal steps necessary to update the app on the K8s cluster.

The `service-definition.yaml` and `deployment-definition.yaml` files can be found inside the folder `python-app-src` alongside the python application files `helloworld.py` and `HelloWorld.class` and the `Dockerfile`.

## Change the message inside the `helloworld.py` file.

"Hello World!" to "Hello Luxembourg!"

## Rebuild the image (mind the dot at the end):

`docker build -t image-name: tag-name .`

`docker build -t hwpython:newest .`

## Display all Docker images, check if the image hwpython exists and see the IMAGE ID:

`docker images`

## Push the modified image to the Docker Hub repository

`docker push username/app-name`

`docker push dmarinova1/hwpython`

## Launch Minikube if not already done so

`minikube start`

## Set the Minikube context to determine which cluster kubectl is interacting with:

`kubectl config use-context minikube`

## Since we are using Minikube, we build the image using the same Docker host as the Minikube VM. Make sure we are using the Minikube Docker daemon, by running the following:

`eval $(minikube docker-env)`

Note: Later, when we no longer wish to use the Minikube host, we can undo this change by running:

`eval $(minikube docker-env -u).`

## List all running Docker containers

`docker ps`

The ps command provides several columns of information:
Column | Definition 
--- | --- 
`Container ID` | a unique alphanumeric number for each container
`Image` | The base operating system image the container is based on
`Command` | The command that launched the container
`Created` | How long ago the container was created
`Status` | Uptime or downtime
`Ports` | Specifies any ports forwarded to the container for networking
`Name` | A memorable name assigned by the Docker software

-> list latest created container
`docker ps –l`

## Build the Docker image, using the Minikube Docker daemon (mind the dot at the end):

`docker build -t hwpython:newest .`

Note: Now the Minikube VM can run the docker image we have built.

## List existing services:

`kubectl get services`

## List existing deployments:

`kubectl get deployments`

## Delete `deployment-definition.yaml` file:

`kubectl delete deployment deployment-definition.yaml`

## Redeploy the same `yaml` file:

`kubectl create -f deployment-definition.yaml`

## Access the service to see the new message:

`minikube service hello-world-python-service`
