
## Docker Fundamentals
-----------------------------

## 1. What is Docker?

Docker is a containerized tool , that help you build and run applications without  platform dependencies .
      
## 2. Why Do We Use Docker?
      
## 3. How Does Docker Work?

## Docker – Why We Use It
##  Dockerfile
## docker image,
## docker container,
## docker registry
  # Docker Fundamentals

 # Docker – Real-World Example

## The Problem

Suppose a developer creates an application on a **Windows laptop**.

The application is developed using **Python 3.9**.

The application also requires:

- A particular Python library
- Some specific permissions
- Specific dependencies
- A specific environment configuration

The application works perfectly on the developer's laptop.

For example:

- **OS:** Windows
- **Python:** 3.9
- **Username:** Admin
- **Required libraries:** Available
- **Required permissions:** Available

The developer thinks:

> "If the application works on my machine, it should also work on my friend's machine."

But when the developer gives the application to his friend, it does not work.

The friend's system is different:

- **OS:** Linux
- **Python:** 3.14
- **Username:** Shubham
- **Required libraries:** Not installed
- **Required dependencies:** Missing
- **Environment:** Different

So the developer says:

> "It works on my machine, but it does not work on the client's system."

This is a common problem in software development.

---

# How Does Docker Solve This Problem?

This is where **Docker** is useful.

Docker allows us to package an application together with its required environment and dependencies.

We can create a **Docker Container** for the application.

Inside the container, we can define the environment required by the application, such as:

- Required OS-level environment
- Required Python version
- Required libraries
- Required dependencies
- Required configuration
- Required permissions and access

For example:


Docker Container
│
├── Application
├── Python 3.9
├── Required Libraries
├── Required Dependencies
├── Configuration
└── Required Environment

## Important Terms
** Docker engine: **

Docker is an engine that runs containerd.

It uses core container technology to create, manage, and run containers.

To access and manage these containers, the Docker daemon runs in the background.

The Docker client is the command-line interface (CLI) through which the user gives commands to Docker.

Docker Registry is also a part of the Docker ecosystem. It is used to store and distribute Docker images.

## why not vertulization - 
*  dedicated resources 
* resources wasteages 
*  host has hypervisior installed 
*  multiple os images insatalled 
*  storage cost increaded 

## why containerization(Docker)-

*  shared resources
*  resources utilization 
*  docker engine takes the host OS
* in window (docker desktop)

## Does docker contaciner have an os of there own ?
* NO , docker container donot have their own os .

# Docker Engine
* containerd(core container technology)
* dockerd(docker daemon)
* docker client (user gives commands )
* Docker registry

  The Docker client communicates with the Docker daemon. The Docker daemon then creates and manages containers based on the commands received from the client.

 A **Dockerfile** is used to build a **Docker image**.
A **Docker container** is created from a Docker image.
The **application runs inside the container**.

A container does not have its own complete operating system. It **shares the host OS kernel** while keeping the application and its dependencies isolated.

The process of creating and running applications in containers is called **containerization**.

**Docker** is a containerization platform/tool used to create, run, and manage containers.


  docker file ├── docker image├── docker container 

**docker search**  is a Docker command used to search for Docker images on Docker Hub.

docker run hello-world — Here, hello-world is the image name.
The docker run command creates a container from the image and runs the container.
In simple words:

Docker Image → Container → Application runs inside the container.

docker run -it ubuntu bash

Docker client sends the command to the Docker daemon.
docker run creates a container from the specified image and starts it.
-it means interactive terminal (-i = interactive, -t = terminal).
ubuntu is the Docker image name.
bash is the command that runs inside the container.
In simple flow:

Docker Client → Docker Daemon → Ubuntu Image → Container → Bash Shell


A command can run on any system that supports Docker. You can run an Ubuntu container locally using Docker.


for EC2

docker ps-- permision denaid
sudo usermod -aG docker $USER
newdrp docker
docker ps
------
docker run -it ubantu bash
run.....


Task 1: Create a Container from an Image

First, search for the Nginx image on Docker Hub:

docker search nginx

Then, create and run a container from the Nginx image:

docker run nginx

Flow:

Docker Hub → Nginx Image → docker run nginx → Nginx Container

Docker containers are **isolated environments**. By default, services running inside a container are not directly accessible from outside the container.

If we want to make a container's application accessible through the host machine, we can use **port mapping**.

For example:

```bash
docker run -p 80:80 nginx
```

Here:

* **First `80`** = Host port
* **Second `80`** = Container port
* **`nginx`** = Image name

This maps **Host Port 80 → Container Port 80**, allowing users to access the Nginx application through the host.

**Important:** Port mapping is used for **network access/communication**, not for sharing general resources.
Simple flow:
User → Host Port 80 → Container Port 80 → Nginx


If you want the container to run in detached mode (in the background), use the -d option.

Example:

docker run -d -p 80:80 nginx
-d → Detached mode (runs in the background)
-p 80:80 → Maps host port 80 to container port 80
nginx → Image name


If you want to give the container a custom name, use the --name option.

docker run -d -p 80:80 --name nginx-demo nginx

Here:

-d → Runs the container in detached mode
-p 80:80 → Maps host port 80 to container port 80
--name nginx-demo → Gives the container the name nginx-demo
nginx → Image name

Flow:
nginx Image → nginx-demo Container → Port 80 → Nginx


example--

f you mean docker run -e MYSQL_..., then -e is used to set an environment variable inside the container.

For example:

docker run -e MYSQL_ROOT_PASSWORD=1234 mysql

Here:

docker run → Creates and starts a container
-e → Sets an environment variable
MYSQL_ROOT_PASSWORD=1234 → Sets the MySQL root password
mysql → MySQL Docker image
Important: -e tabhi useful hai jab application/image us environment variable ko read karti ho.


docker ps

docker ps command se currently running containers ki list dekh sakte hain.

docker ps
docker stop

docker stop command se running container ko stop karte hain.

docker stop nginx-demo

Simple flow:
docker ps
   ↓
Running containers dekho
   ↓
docker stop nginx-demo
   ↓
Container stop ho gaya


Extra: Sabhi containers dekhne ke liye, including stopped containers:

docker ps -a


docker rm

docker rm command se stopped container ko delete/remove karte hain.

Example:

docker rm nginx-demo

Yahan nginx-demo container ka name hai.

docker ps

docker ps se running containers ki list dekhte hain:

docker ps

Stopped containers bhi dekhne ke liye:

docker ps -a
Simple flow:
docker ps
   ↓
Running container dekho
   ↓
docker stop nginx-demo
   ↓
Container stop
   ↓
docker rm nginx-demo
   ↓
Container delete

Important: docker rm image ko delete nahi karta, sirf container ko delete karta hai.


ocker kill

docker kill command se running container ko immediately forcefully stop karte hain.

docker kill nginx-demo

Yahan nginx-demo container ka name hai.

docker stop vs docker kill
docker stop → Container ko gracefully stop karta hai; application ko shutdown hone ka time milta hai.
docker kill → Container ko immediately forcefully stop karta hai.

Simple:
docker stop = normal stop
docker kill = force stop


We start with the source code of an application. Using Docker, we build the application into a Docker image.

The ultimate goal is to run the application.

The application runs inside a Docker container. A container is created from a Docker image, and a Docker image is built using a Dockerfile.

Docker Flow

Source Code → Dockerfile → Docker Image → Docker Container → Application Runs

In simple words:

Dockerfile builds the image → Image creates the container → Application runs inside the container.
