# BSP-S6-Containerisation
This is a Bachelor Semester Project on "Containerisation of services" with domains on Cloud Computing, Docker, Kubernetes

# **Docker Tutorial**
This tutorial was built using [Java Code Geeks Docker Hello World Example](https://examples.javacodegeeks.com/devops/docker/docker-hello-world-example/) and [Docker for Mac Docs](https://docs.docker.com/docker-for-mac/)

## Objectives:
The objectives are:
-	To setup Docker 
-	To run Docker container and build an image

## Docker setup

### 1.	Go to Docker Hub and create an account if you do not have any.
https://hub.docker.com
### 2.	Download Docker Desktop for the system you are operating on (Windows, macOS, etc.) 
### 3.	Install Docker Desktop.
- Double-click Docker.dmg to open the installer, drag the Docker icon to the Applications folder.
- Double-click Docker.app in the Applications folder to start Docker. You are prompted to authorize Docker.app with your system password after you launch it. Privileged access is needed to install networking components and links to the Docker apps.
- The Docker menu in the top status bar indicates that Docker Desktop is running, and accessible from a terminal.
- Once you are done installing Docker, test your Docker installation by running the following Docker hello-world image:
``` $ docker run hello-world
    Unable to find image 'hello-world:latest' locally
    latest: Pulling from library/hello-world
    03f4658f8b78: Pull complete
    Digest: sha256:8be990ef2aeb16dbcb9271ddfe2610fa6658d13f6dfb8bc72074cc1ca36966a7
    Status: Downloaded newer image for hello-world:latest
	
    Hello from Docker.
    This message shows that your installation appears to be working correctly.
   	...
```
    
### 4.	Get started with Docker Desktop for Mac
- Running our first “Hello World” container using an Alpine Linux container (a lightweight linux distribution) on our system. We run the following in our terminal:
```$ docker pull alpine```
The pull command fetches the alpine image from the Docker registry and saves it in our system. We can use the docker images command to see a list of all images on your system.
```$ docker images```
![DockerImages](docker-images.png)

We can run a Docker container based on this image. To do that we are going to use the docker run command:

```$ docker run alpine ls -l
total 56
drwxr-xr-x    2 root     root          4096 Jan  2 21:52 bin
drwxr-xr-x    5 root     root           340 Feb 18 08:24 dev
drwxr-xr-x    1 root     root          4096 Feb 18 08:24 etc
drwxr-xr-x    2 root     root          4096 Jan  2 21:52 home
drwxr-xr-x    5 root     root          4096 Jan  2 21:52 lib
......
......
```
When we run $ docker run alpine with command (ls -l), Docker starts the specified command and shows the listing.

### 5. Get a “Hello, world” Printed from Another Basic Docker Image:
1)
```
$ docker run alpine echo "hello from alpine"
hello from alpine
```

2)
```$ docker run alpine:latest "echo" "Hello, World"```

The second command downloads the Alpine baseimage the first time and creates a Docker container. Then runs the container and executes the echo command. The echo command echoes the “Hello, World” string.  As a result, you should see the output as below.

### 6. Docker containers

Using the docker ps command we can see all containers that are currently running.

```
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```
Since no containers are running there is a blank line. A more useful variant: 
```docker ps -a```
![DockerContainers](docker-ps-a.png)
What we see above is a list of all containers that we ran. Notice that the STATUS column shows that these containers exited a few minutes/seconds ago. 

There is a way to run more than just one command in a container with:
```$ docker run -it alpine /bin/sh```
![DockerCommands](docker-it.png)
Running the run command with the -it we deploy flags interactivity in the container. Now we can run as many commands in the container as we want. Take some time to run your favorite commands.
To find out more about run command, we can use docker run --help to see a list of all flags it supports. 

### 7. Create HelloWorld.java

First, we create a simple Java program that prints “Hello, World” (a program very closely resembling the one provided in the Official Java tutorial).  Open up any text editor and enter the following code:
```	
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World");
    }
}
```
- Save the file as HelloWorld.java.  
- compile this file using the Java compiler to create the class file Helloworld.class
```$ javac HelloWorld.java```
To execute the Hello World with Java:
![JavaExecuteHelloWorld](javac-hw.png)

However, the aim is to run this from within a Docker container.  To accomplish that we need to create a Docker image. 

### 7. Create a Dockerfile in order to create a Docker image.
A Dockerfile defines a docker image.

We shall use the Command Line tool.

- Open Terminal. 
- Go to your Desktop. 
- Create a folder called “DockerFiles” with the command ```mkdir DockerFiles```
- Go inside the folder with command ```cd DockerFiles ```
- Create a Dockerfile with command ```touch Dockerfile ```
- Edit the Dockerfile with command ```vim Dockerfile```
- Inside the vim editor press "I" on the keyboard to go inside the “insert” mode. Type the instructions:

```
# get the Alpine baseimage
FROM alpine:latest
# add HelloWorld class to the image with the same name
ADD HelloWorld.class HelloWorld.class
# install JRE environment using OpenJDK
RUN apk --update add openjdk8-jre
# give command to execute when this image is run
ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "HelloWorld"]
```
Press Esc and type ```:wq!``` to exit
To see contents of Dockerfile type ```cat Dockerfile```
![Dockerfile](dockerfile.png)
- Build/Create the image using command with a dot at the end (if inside the repository of the Dockerfile): 
```$ docker build .```
- Or, if not inside the location of Dockerfile, type:
```$ docker build /Users/username/Desktop/DockerFiles/ .```
- Or tag your image/give your image name (syntax format is docker build -t imageName:imageTag), i.e. with command:
```$ docker build --tag "docker-hello-world:latest" .```
- Run the command. See message “Successfully built” followed by the image ID
![Dockerfile](docker-build.png)

- Check your images with ```docker images``` and note that your image is there.
- Run your image and see the message “Hello, World” displayed:
```$ docker run docker-hello-world:latest```
