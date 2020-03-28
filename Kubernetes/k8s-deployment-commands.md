This file contains useful k8s deployment commands. [Reference 1.](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-strong-getting-started-strong-)
[Reference 2.](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

## Create a deployment
```
$ create -f FILENAME
kubectl create -f deployment-definition.yaml
```
## Apply 
-> Create a deployment based on the YAML configuration file, i.e 'apply' a configuration to a resource by filename or stdin. JSON and YAML formats are accepted.
```
$ apply (-f FILENAME | -k DIRECTORY)
kubectl apply -f deployment-definition.yaml
```
## List existing deployments
```
kubectl get deployments
```
## List a particular deployment
```
kubectl get deployment hello-world-deployment
```

## Edit the deployment 'deployment-definition' in YAML and save the modified config in its annotation:
```
kubectl edit deployment/deployment-definition -o yaml --save-config
```
## Create a service for a hello-world-deployment deployment (e.g. which serves on port 3333 and connects to the containers on port 8000)
```
$ expose (-f FILENAME | TYPE NAME) [--port=port] [--protocol=TCP|UDP|SCTP] [--target-port=number-or-name] [--name=name] [--external-ip=external-ip-of-service] [--type=type]

kubectl expose deployment hello-world-deployment --port=3333 --target-port=8000
```
## Update
-> Update resource fields; ```--force``` deletes and re-creates the resource:
```
kubectl replace -f deployment-definition.yaml --force
```
-> Check the history of deployments including the revision 
```
kubectl rollout history deployment/hello-world-deployment                     
```
-> Rollback to the previous deployment
```
kubectl rollout undo deployment/hello-world-deployment                        
```

-> Rollback to a specific revision
```
kubectl rollout undo deployment/hello-world-deployment --to-revision=2         
```

-> Watch rolling update status of "hello-world-deployment" deployment until completion
```
kubectl rollout status -w deployment/hello-world-deployment                   
```

-> Rolling restart of the "hello-world-deployment" deployment
```
kubectl rollout restart deployment/hello-world-deployment                   
```

## Scale
```
$ scale [--resource-version=version] [--current-replicas=count] --replicas=COUNT (-f FILENAME | TYPE NAME)
```
-> Set a new size for a Deployment, scale a resource:
```
kubectl scale --replicas=2 -f deployment-definition.yaml
```
-> Auto scale a deployment "hello-world-deployment"
```
kubectl autoscale deployment hello-world-deployment --min=2 --max=10
```

## Delete
```
$ delete ([-f FILENAME] | [-k DIRECTORY] | TYPE [(NAME | -l label | --all)])

kubectl delete deployment deployment-definition.yaml
```
