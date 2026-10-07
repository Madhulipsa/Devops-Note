
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

# Docker Notes

## Docker Image → Container → Application

```bash
docker run hello-world
```

Here, `hello-world` is the image name.

The `docker run` command creates a container from the image and runs the container.

### In simple words:

```text
Docker Image → Container → Application runs inside the container
```

---

## docker run -it ubuntu bash

```bash
docker run -it ubuntu bash
```

Docker client sends the command to the Docker daemon.

`docker run` creates a container from the specified image and starts it.

`-it` means interactive terminal:

* `-i` = interactive
* `-t` = terminal

`ubuntu` is the Docker image name.

`bash` is the command that runs inside the container.

### In simple flow:

```text
Docker Client → Docker Daemon → Ubuntu Image → Container → Bash Shell
```

A command can run on any system that supports Docker.

You can run an Ubuntu container locally using Docker.

---

# For EC2

```bash
docker ps
```

If you get:

```text
permission denied
```

Run:

```bash
sudo usermod -aG docker $USER
```

Then:

```bash
newgrp docker
```

Now:

```bash
docker ps
```

---

## Run Ubuntu Container

```bash
docker run -it ubuntu bash
```

Run the command and enter inside the Ubuntu container.

---

# Task 1: Create a Container from an Image

First, search for the Nginx image on Docker Hub:

```bash
docker search nginx
```

Then, create and run a container from the Nginx image:

```bash
docker run nginx
```

### Flow:

```text
Docker Hub → Nginx Image → docker run nginx → Nginx Container
```

---

# Docker Port Mapping

Docker containers are **isolated environments**.

By default, services running inside a container are not directly accessible from outside the container.

If we want to make a container's application accessible through the host machine, we can use **port mapping**.

For example:

```bash
docker run -p 80:80 nginx
```

Here:

* **First `80`** = Host port
* **Second `80`** = Container port
* **`nginx`** = Image name

This maps:

```text
Host Port 80 → Container Port 80
```

allowing users to access the Nginx application through the host.

**Important:** Port mapping is used for **network access/communication**, not for sharing general resources.

### Simple flow:

```text
User → Host Port 80 → Container Port 80 → Nginx
```

---

# Detached Mode

If you want the container to run in detached mode (in the background), use the `-d` option.

Example:

```bash
docker run -d -p 80:80 nginx
```

* `-d` → Detached mode (runs in the background)
* `-p 80:80` → Maps host port 80 to container port 80
* `nginx` → Image name

---

# Custom Container Name

If you want to give the container a custom name, use the `--name` option.

```bash
docker run -d -p 80:80 --name nginx-demo nginx
```

Here:

* `-d` → Runs the container in detached mode
* `-p 80:80` → Maps host port 80 to container port 80
* `--name nginx-demo` → Gives the container the name `nginx-demo`
* `nginx` → Image name

### Flow:

```text
Nginx Image → nginx-demo Container → Port 80 → Nginx
```

---

# Environment Variable `-e`

If you mean `docker run -e MYSQL_...`, then `-e` is used to set an environment variable inside the container.

For example:

```bash
docker run -e MYSQL_ROOT_PASSWORD=1234 mysql
```

Here:

* `docker run` → Creates and starts a container
* `-e` → Sets an environment variable
* `MYSQL_ROOT_PASSWORD=1234` → Sets the MySQL root password
* `mysql` → MySQL Docker image

**Important:** `-e` tabhi useful hai jab application/image us environment variable ko read karti ho.

---

# docker ps

`docker ps` command se currently running containers ki list dekh sakte hain.

```bash
docker ps
```

---

# docker stop

`docker stop` command se running container ko stop karte hain.

```bash
docker stop nginx-demo
```

### Simple flow:

```text
docker ps
   ↓
Running containers dekho
   ↓
docker stop nginx-demo
   ↓
Container stop ho gaya
```

---

# docker ps -a

Sabhi containers dekhne ke liye, including stopped containers:

```bash
docker ps -a
```

---

# docker rm

`docker rm` command se stopped container ko delete/remove karte hain.

Example:

```bash
docker rm nginx-demo
```

Yahan `nginx-demo` container ka name hai.

### Simple flow:

```text
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
```

**Important:** `docker rm` image ko delete nahi karta, sirf container ko delete karta hai.

---

# docker kill

`docker kill` command se running container ko immediately forcefully stop karte hain.

```bash
docker kill nginx-demo
```

Yahan `nginx-demo` container ka name hai.

## docker stop vs docker kill

`docker stop` → Container ko gracefully stop karta hai; application ko shutdown hone ka time milta hai.

`docker kill` → Container ko immediately forcefully stop karta hai.

### Simple:

```text
docker stop = normal stop
docker kill = force stop
```

---

# Complete Docker Application Flow

We start with the source code of an application.

Using Docker, we build the application into a Docker image.

The ultimate goal is to run the application.

The application runs inside a Docker container.

A container is created from a Docker image, and a Docker image is built using a Dockerfile.

## Docker Flow

```text
Source Code → Dockerfile → Docker Image → Docker Container → Application Runs
```

### In simple words:

```text
Dockerfile builds the image
        ↓
Image creates the container
        ↓
Application runs inside the container
```

# Deploy an Application Using Docker

## Ultimate Goal

Humein ek application ko Docker ki help se deploy karna hai.

Sabse pehle humein **application ka source code** chahiye.

Us source code ko Docker ki help se **build** karna hai.

Ultimate aim:

```text
Application Code
       ↓
Dockerfile
       ↓
Docker Image
       ↓
Docker Container
       ↓
Application Runs
```

### Simple Concept

> **Dockerfile se Image banti hai → Image se Container banta hai → Container ke andar Application run hoti hai.**

---

# Step 1: Create a Directory

Sabse pehle ek directory banayenge.

```bash
mkdir python
```

Directory ke andar jayenge:

```bash
cd python
```

Check karne ke liye:

```bash
ls
```

---

# Step 2: Get Application Code from GitHub

Ab humein GitHub se application ka source code lena hai.

GitHub repository ko HTTP/HTTPS ke through clone karenge:

```bash
git clone <https-url>
```

Example:

```bash
git clone https://github.com/username/application.git
```

Enter press karne ke baad GitHub ka code system mein aa jayega.

### Flow

```text
GitHub
   ↓
git clone <https-url>
   ↓
Application Source Code
   ↓
Local Machine / EC2
```

---

# Step 3: Application Code Check

Code clone hone ke baad application directory mein jayenge:

```bash
cd application
```

Files check karne ke liye:

```bash
ls
```

Ab humein application ka code mil gaya.

```text
Application Source Code
        ↓
     We have Code
        ↓
Now we need to build it using Docker
```

---

# Step 4: Create Dockerfile

Sabse pehle Dockerfile banayenge.

```bash
vim Dockerfile
```

Dockerfile ke andar hum application ko build karne ke instructions denge.

---

# Step 5: Dockerfile

Example:

```dockerfile
# Bring Patila (Base Image)
FROM python:3.14

# Work inside /app
WORKDIR /app

# Add Doodh + Pani + Chai Patti
# Copy application code
COPY . .

# Add Chini + Elaichi + Adrak
# Install dependencies
RUN pip install -r requirements.txt

# Chai kaha milegi?
# Which port will this application run on?
EXPOSE 80

# Gas ON - Run the application
CMD ["python", "run.py"]
```

---

# Dockerfile Explanation Using Chai Example ☕

## 1. FROM

```dockerfile
FROM python:3.14
```

### Chai Example

```text
Patila
  ↓
Python 3.14 Base Image
```

`FROM` tells Docker which **base image** to use.

Here:

```text
python:3.14
```

is the base image.

---

# 2. WORKDIR

```dockerfile
WORKDIR /app
```

This tells Docker that `/app` will be the working directory inside the container.

### Chai Example

```text
Patila ke andar kaam karne ki jagah
        ↓
       /app
```

---

# 3. COPY

```dockerfile
COPY . .
```

This copies the application source code into the Docker image.

### COPY Syntax

```text
COPY <source> <destination>
```

Here:

```text
Source      → .
Destination → .
```

### Chai Example

```text
Doodh + Pani + Chai Patti
        ↓
Application Code
        ↓
COPY . .
```

---

# 4. RUN

```dockerfile
RUN pip install -r requirements.txt
```

This installs the dependencies required by the application.

### Chai Example

```text
Chini
Elaichi
Adrak
   ↓
Application Dependencies
   ↓
RUN pip install -r requirements.txt
```

`requirements.txt` contains the Python packages/dependencies required by the application.

---

# 5. EXPOSE

```dockerfile
EXPOSE 80
```

This tells Docker that the application is intended to listen on port `80`.

### Chai Example

```text
Chai kaha milegi?
        ↓
Port 80
```

So:

```text
EXPOSE 80
↓
Application Port
```

---

# 6. CMD

```dockerfile
CMD ["python", "run.py"]
```

This tells Docker what command to run when the container starts.

### Chai Example

```text
Gas ON 🔥
    ↓
Chai banana start
    ↓
Application Run
```

Here:

```text
python run.py
```

runs the Python application.

> `run.py` is the entry point provided by the developer/application.

---

# Complete Chai → Docker Concept ☕

```text
                 CHAI RECIPE
                     ↓
        ┌─────────────────────────┐
        │ FROM python:3.14        │
        │ Patila                  │
        └─────────────────────────┘
                     ↓
        ┌─────────────────────────┐
        │ WORKDIR /app            │
        │ Kaam karne ki jagah     │
        └─────────────────────────┘
                     ↓
        ┌─────────────────────────┐
        │ COPY . .                │
        │ Doodh + Pani + Patti    │
        └─────────────────────────┘
                     ↓
        ┌─────────────────────────┐
        │ RUN pip install         │
        │ Chini + Elaichi + Adrak │
        └─────────────────────────┘
                     ↓
        ┌─────────────────────────┐
        │ EXPOSE 80               │
        │ Chai kaha milegi?       │
        └─────────────────────────┘
                     ↓
        ┌─────────────────────────┐
        │ CMD ["python","run.py"] │
        │ Gas ON 🔥               │
        └─────────────────────────┘
                     ↓
              APPLICATION RUNS
```
Step 6: Build Docker Image

Dockerfile ke basis par image banayenge:

docker build -t devboard .
Breakdown
docker build
     ↓
Docker image build karo

-t devboard
     ↓
Image ka naam = devboard

.
     ↓
Current directory mein Dockerfile use karo

Check image:

docker images
Step 7: Run Docker Container

Agar application port 80 par run kar rahi hai:

docker run -p 80:80 -d devboard
Meaning
-p 80:80

Host Port       Container Port
    80     →        80

Check running container:

docker ps
🌐 Application ko IP Address se Access Karna

Agar application ko sirf localhost par nahi, balki server/EC2 ke IP address se access karna hai, application ko 0.0.0.0 par bind karna zaroori hai.

Example:

CMD ["npm", "run", "dev", "--", "--host", "0.0.0.0"]

Agar application port 5173 use karti hai:

docker run -p 5173:5173 -d devboard

Then:

http://YOUR-IP:5173

Example:

http://13.234.56.78:5173

For port 80:

docker run -p 80:80 -d devboard

Then:

http://YOUR-IP

AWS EC2 use kar rahe ho to required port ko Security Group mein allow karna bhi zaroori hai.
---

# Complete Docker Deployment Flow

```text
GitHub
   ↓
git clone <https-url>
   ↓
Application Source Code
   ↓
vim Dockerfile
   ↓
Write Dockerfile
   ↓
docker build
   ↓
Docker Image
   ↓
docker run
   ↓
Docker Container
   ↓
Application Runs
```

## Ultimate Aim

```text
Source Code
     ↓
Dockerfile
     ↓
Docker Image
     ↓
Docker Container
     ↓
Application Runs Inside Container
```

> **Code chahiye → Dockerfile se code build karenge → Docker Image banegi → Image se Container banega → Container ke andar Application run hogi.**
