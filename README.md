# BSP-S6-K8s-Fundamentals
This is a Bachelor Semester Project on "Containerisation of services" with domains on Cloud Computing, Docker, Kubernetes

## Inside the Docker folder you can find:
- a tutorial on setting up the Docker platform and building your first container. 
- images used for the tutorial setup
- Docker ```commands.md``` to creating a Dockerfile, building a Docker image, pushing it to Docker Hub repo, running an image inside a container
- produced resources located in ```src``` folder

The ```glossary-v.#.md``` file is a list of terms with definitions that are collected from official documentations on container services. The v.# indicates the version number, starting from v-0.1.

## Inside the Kubernetes folder you can find:
The ```k8s-app-deployment.md``` which contains a tutorial on how to create a local kubernetes cluster using Minikube and Docker Container Image on Mac. 

The ```k8s-deployment-commands.md``` contains most often used commands for deployment and a short description.

The ```k8s-update-app.md``` contains ordered steps, in case we want to change a line inside the Python application file and how to update the application on the cluster.

The python-app-src folder contains 2 folders: python and python3. The former is the code for our "Hello Luxembourg!" application. The latter is the source code for our "Hello Germany!" application. We use both simultaneously for the blue/green study case. Otherwise, the "Hello Luxembourg!" source code is the project we deploy both locally with Minikube and in the GCP.

## Inside the GCP folder you can find:
The ```gcp-deployment.md``` that explains how to deploy our simple application on the public cloud. 
The src folder contains our source code.
