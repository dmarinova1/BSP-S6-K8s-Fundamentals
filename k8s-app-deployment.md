# In this tutorial, we test Kubernetes locally on Mac using Minikube and a Docker Container Image.
See this page [Minikube Installation Guide](https://kubernetes.io/docs/tasks/tools/install-minikube/) if you have not yet installed Minikube, in order to follow this tutorial. 

start the Minikube cluster:

```minikube start```

set the Minikube context to determine which cluster kubectl is interacting with:

```kubectl config use-context minikube```

to verify that kubectl is configured to communicate with our cluster:

```kubectl cluster-info```

once we have configured Minikube to run Kubernetes locally, we can open the Kubernetes dashboard in a browser using the following command:

```minikube dashboard```

Since we are using Minikube, instead of pushing our Docker image to a registry, we build the image using the same Docker host as the Minikube VM, so that the images are automatically present.
To do this we need to make sure we are using the Minikube Docker daemon, by running the following:

```eval $(minikube docker-env)```

Note: Later, when we no longer wish to use the Minikube host, we can undo this change by running:

```eval $(minikube docker-env -u).```

After we have written our application in a filename "helloworld.py" and saved it in a project folder "python", we create our Dockerfile containing commands for our Docker image. 
Then we build our Docker image, using the Minikube Docker daemon (mind the dot at the end):

```docker build -t hwpython:newest .```

Now the Minikube VM can run the docker image we have built.

# Create a Deployment

We can use the ```kubectl run``` command to create a Deployment that manages a Pod. 
The Pod runs a Container based on our ```hwpython:newest``` Docker image. Set the ```--image-pull-policy``` flag to ```Never``` which means that it will always use the local image, rather than pulling it from our Docker registry.

```kubectl run hwpython --image=hwpython:newest --port=3333 --image-pull-policy=Never```

## Deployment: 

```kubectl get deployments```

## View the pod:

```kubectl get pods```

## View cluster events:

```kubectl get events```

## Create a Service:
By default, the Pod is only accessible by its internal IP address within the Kubernetes cluster. 
To access the hwpython Container Deployment from outside the Kubernetes virtual network, we expose the Pod as a Service:

```kubectl expose deployment hwpython --type=LoadBalancer --port=3333```

The ```--type=LoadBalancer``` flag indicates that we want to expose our service outside of the cluster.
On Minikube, the LoadBalancer type makes the Service accessible through the ```minikube service``` command.

**Note**: Kubernetes ServiceTypes allow us to specify what kind of Service we want. The default is ClusterIP.

-> Type values and their behaviors are:
- **ClusterIP**: Exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster. This is the default ServiceType.
- **NodePort**: Exposes the Service on each Node’s IP at a static port (the NodePort). A ClusterIP Service, to which the NodePort Service routes, is automatically created. We'll be able to contact the NodePort Service, from outside the cluster, by requesting NodeIP:NodePort.
- **LoadBalancer**: Exposes the Service externally using a cloud provider’s load balancer. NodePort and ClusterIP Services, to which the external load balancer routes, are automatically created.
- **ExternalName**: Maps the Service to the contents of the externalName field, by returning a CNAME record with its value. No proxying of any kind is set up.

Ref: [K8s Services](https://kubernetes.io/docs/concepts/services-networking/service/)

## View the kubectl configuration:

```kubectl config view```

## View the Service:

```kubectl get service```

## the Service accessible through the minikube service command:

```minikube service hwpython```

This automatically opens up a browser window using the local IP address that serves our app and shows the “Hello World” message.

*or* using the command to obtain access to the services which prints out the IP address of Minikube VM and the port the service is mapped to:

```minikube service hwpython --url```

we can copy the address and go to a web browser to see the page output. 

## If we want to delete the hwpython Service:

```kubectl delete services hwpython```

## If we want to remove the deployment which will also remove the pod that it was managing:

`kubectl delete deployment hwpython`

## Get the IP of your `minikube` host:

`minikube ip`

## Stop the local Minikube cluster:

```minikube stop```
