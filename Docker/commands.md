#create a general folder for all your projects, e.g. entitled "Dockerfiles"

#inside Dockerfiles, for each project, create inidividual folders.

#navigate to the location of the general folder "Dockerfiles" (mine is located on the Desktop)

```cd Desktop```

```cd Dockerfiles```

#create a new directory to hold your project on Python

mkdir project-folder-name, e.g. ```mkdir python```

#go inside the newly created project directory

cd project-folder-name, e.g. ```cd python```

#create an empty Dockerfile

```touch Dockerfile```

#use a text editor (either Vim or Nano) to open the Dockerfile and edit it
```vim Dockerfile``` or ```nano Dockerfile```

#I used vim editor. Now, click on ```I``` (Insert) letter on the keyboard to edit the text file.

#Write the content inside the Dockerfile:
```
FROM python:3
ADD helloworld.py /
RUN pip install flask
RUN pip install flask_restful
EXPOSE 3333
CMD [ "python", "./helloworld.py"]
```

#Once done, click on ```Esc``` and write ```:wq!``` to exit

#view the Dockerfile content to make sure it all worked properly:

```cat Dockerfile```

# Build the Docker image
#build the image from the Dockerfile, tag it by giving it a name and a tag name, followed by a space and a dot.

```docker build -t image-name: tag-name .```

```docker build -t hwpython: newest .```

#display all Docker images, check if the image hwpython exists and see its ID

```docker images```

# How to push to Docker Hub repository (first create a repository with the name 'hwpython' on Docker Hub)
#Log in on https://hub.docker.com/
#Click on Create Repository.
#Choose a name (e.g. hwpython) and a description for your repository and click Create.

#go back to your Terminal and tag your image

```docker tag ID-image dmarinova1/hwpython:newest```

#Push your image to the repository you created

```docker push dmarinova1/hwpython```

# Running the image inside the Hello World Python container
#run a command in a container, publishing the container's port(s) to the host with the option ```-p```

#the code uses port 3333, and it is mapped to the local port 3333

```docker run -p 3333:3333 hwpython:newest```

#the Terminal app displays:
> Running on http://0.0.0.0:3333/

#open a new Terminal window and type the command below to see the "Hello, World!" message:

```curl http://0.0.0.0:3333/```

#curl is a tool to transfer data from or to a server, using a protocol (to install it using Homebrew type in Terminal screen brew install curl and press enter/return key)
