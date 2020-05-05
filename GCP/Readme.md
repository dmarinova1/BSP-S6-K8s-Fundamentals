# How to deploy a Python web app on Google Cloud Platform.
## Before following this steps, it is assumed that a GCP account has already been set up.

## Create a cluster. Click on the 3 bar icon, top left corner and select "Kubernetes Engine" -> "Clusters" and create your cluster, giving it a name and choosing the default settings.

#open the GCP console: https://console.cloud.google.com

#create a project, select "Project" -> "Create Project"

#click on top right icon to active the google cloud shell.

#create a general folder for your project, e.g. entitled "python". For this, click on "Open Editor" -> "File" -> "New folder". Then create the necessary files for the applications. 
- main python code for the web app, "hellolux.py"
- requirements.txt = specifies additional libraries needed for our application to be deployed
- Dockerfile
3 manifest files:
- deployment.yaml
- service.yaml
- app.yaml = contains the configuration data


#Dockerfile content:
```
FROM python:3
ADD hellolux.py /
RUN pip install flask
EXPOSE 3333
CMD [ "python", "./hellolux.py"]
```

#hellolux.py content:
```
from flask import Flask

app = Flask(__name__)


@app.route('/')
def hello():
    return 'Hello Luxembourg!'


if __name__ == '__main__':
    app.run(host='0.0.0.0', port=3333, debug=True)
```

#deployment.yaml content:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-lux-deployment
  labels:
    app: hellolux2
spec:
  replicas: 1
  selector:
    matchLabels:
      app: helloluxembourg
  template:
    metadata:
      labels:
        app: helloluxembourg
    spec:
      containers:
      - name: hello-lux-container1
        image: gcr.io/my-test-project-240511/hellolux:latest
        ports:
        - containerPort: 3333
```
#service.yaml content:
```
apiVersion: v1
kind: Service
metadata:
  name: hello-lux-service3
spec:
  selector:
    app: helloluxembourg
  type: LoadBalancer
  ports:
    - name: hello-lux-port
      port: 80
      targetPort: 3333
```
#app.yaml content:
```
runtime: python
env: flex 
entrypoint: gunicorn -b :$PORT hellolux:app

runtime_config:
    python_version: 3
```  

#requirements.txt content:
``` 
Flask==1.1.1
gunicorn==20.0.4
``` 

#go back to the cloud shell

#list the content on your repository

```ls```

#navigate to the location of the folder "python"
```cd python```

#to deploy the application, run the following command:

```gcloud app deploy```

#it takes several minutes when you deploy for the first time, otherwise for subsequent deployments it is faster

#copy the provided URL where the service has been deployed and paste it in a new browser tab. OR type the command to be displayed the URL or directly opened in the browser:
```gcloud app browse```

#the URL returns the string "Hello Luxembourg"
