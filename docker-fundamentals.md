
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
# Step 6: Build Docker Image

Dockerfile ke basis par Docker image banayenge:

```bash
docker build -t devboard .
```

### Breakdown

```text
docker build
     ↓
Docker image build karo

-t devboard
     ↓
Image ka naam = devboard

.
     ↓
Current directory mein Dockerfile use karo
```

### Check Docker Image

```bash
docker images
```

Expected:

```text
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
devboard      latest    xxxxxxxxxxxx   ...           ...
```

---

# Step 7: Run Docker Container

Agar application **container ke andar port 80** par run kar rahi hai:

```bash
docker run -p 80:80 -d devboard
```

### Port Mapping

```text
-p 80:80

Host Port          Container Port
    80       →          80
```

### Meaning

```text
Browser
   ↓
Host / EC2 Port 80
   ↓
Docker Port Mapping
   ↓
Container Port 80
   ↓
Application
```

### Check Running Container

```bash
docker ps
```

---

# 🌐 Access Application Using IP Address

Agar application ko **localhost ke bajay server/EC2 ke IP address** se access karna hai, application ko `0.0.0.0` par bind karna zaroori hai.

### Example: Node.js / Vite Application

```dockerfile
CMD ["npm", "run", "dev", "--", "--host", "0.0.0.0"]
```

`0.0.0.0` ka meaning hai:

```text
Application
     ↓
Listen on all network interfaces
     ↓
Can be accessed through server IP
```

---

# 🚀 If Application Uses Port 5173

Agar application **container ke andar port 5173** par run kar rahi hai:

```bash
docker run -p 5173:5173 -d devboard
```

Ab server ke IP se access kar sakte ho:

```text
http://YOUR-IP:5173
```

Example:

```text
http://13.234.56.78:5173
```

### Flow

```text
Browser
   ↓
http://YOUR-IP:5173
   ↓
Server Port 5173
   ↓
Docker
   ↓
Container Port 5173
   ↓
Application
```

---

# 🌐 If Application Uses Port 80

Agar application **container ke andar port 80** par run kar rahi hai:

```bash
docker run -p 80:80 -d devboard
```

Access:

```text
http://YOUR-IP
```

Example:

```text
http://13.234.56.78
```

### Flow

```text
Browser
   ↓
http://YOUR-IP
   ↓
Server Port 80
   ↓
Docker
   ↓
Container Port 80
   ↓
Application
```

---

# ⚠️ Important: `EXPOSE` vs `-p`

Dockerfile mein:

```dockerfile
EXPOSE 80
```

sirf ye document karta hai ki application **port 80 use karti hai**.

Ye port ko automatically public nahi karta.

Port publish karne ke liye:

```bash
docker run -p 80:80 -d devboard
```

use karna hota hai.

```text
EXPOSE 80
     ↓
Container Port Information

-p 80:80
     ↓
Actually Port Publish / Map
```

---

# ☁️ AWS EC2 Important

Agar application AWS EC2 par chal rahi hai, to EC2 **Security Group** mein required port allow karna hoga.

For port 80:

```text
Inbound Rule
    ↓
Type: HTTP
Port: 80
Source: Required IP / 0.0.0.0/0
```

For port 5173:

```text
Inbound Rule
    ↓
Custom TCP
Port: 5173
Source: Required IP / 0.0.0.0/0
```

---

# 🧠 Final Concept

```text
Application
     ↓
0.0.0.0
     ↓
Container Port
     ↓
docker run -p
     ↓
Host / EC2 Port
     ↓
EC2 Public IP
     ↓
Browser
```

### Example

```text
Application
     ↓
0.0.0.0:5173
     ↓
Docker Container
     ↓
-p 5173:5173
     ↓
EC2 :5173
     ↓
http://EC2-PUBLIC-IP:5173
```
# Step 8: Run Docker Container

Docker image `devboard` se container start karenge.

```bash
docker run -d -p 5173:5173 devboard
```

### Command Breakdown

```text
docker run
    ↓
Create and start a container

-d
    ↓
Run container in background (Detached Mode)

-p 5173:5173
    ↓
Host Port 5173 → Container Port 5173

devboard
    ↓
Docker Image Name
```

---

# Step 9: Check Running Container

Container successfully running hai ya nahi check karne ke liye:

```bash
docker ps
```

Expected output:

```text
CONTAINER ID   IMAGE      PORTS
xxxxxxxxxxxx   devboard   0.0.0.0:5173->5173/tcp
```

### Port Mapping

```text
Host / EC2 Port       Container Port
       5173      →          5173
```

---

# 🌐 Access Application

Agar application AWS EC2 par running hai:

```text
http://YOUR-EC2-PUBLIC-IP:5173
```

Example:

```text
http://13.234.56.78:5173
```

### Complete Flow

```text
Dockerfile
    ↓
docker build -t devboard .
    ↓
Docker Image
    ↓
docker run -d -p 5173:5173 devboard
    ↓
Docker Container
    ↓
EC2 Port 5173
    ↓
EC2 Public IP
    ↓
Browser
    ↓
Application
```

> **Important:** Application ko external IP se access karne ke liye app ko `0.0.0.0` par listen karna chahiye, aur AWS EC2 Security Group mein port `5173` allow hona chahiye.

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

**Code chahiye → Dockerfile se code build karenge → Docker Image banegi → Image se Container banega → Container ke andar Application run hogi.**
# 🚀 Advanced Docker Concepts

# 🚀 Advanced Docker Concepts

The following are the key **advanced Docker concepts**:

* 🏗️ [Multi-Stage Dockerfile](#-multi-stage-dockerfile)
* 💾 [Docker Volumes](#-docker-volumes)
* 🌐 Docker Networking
* 🧩 Docker Compose
* 🤖 Docker Model Runner
* 🧠 AI Models on Docker

---

# 🐳 Multi-Stage Dockerfile

A **multi-stage Docker build** uses multiple `FROM` instructions to separate the application build process from the final runtime image.

### Why Use Multi-Stage Builds?

* Reduce the final Docker image size.
* Keep build tools out of the final image.
* Improve security by including only the required runtime files.
* Make Docker images more efficient.

## 🔹 Stage 1 — Builder Stage

### 1. Bring the Base Image

```dockerfile
FROM python:3.14 AS builder
```

* `FROM` specifies the base image.
* `python:3.14` provides the Python environment.
* `AS builder` names this stage `builder`.

### 2. Create and Set the Working Directory

```dockerfile
WORKDIR /app
```

Creates the `/app` directory if necessary and sets it as the working directory.

### 3. Copy Application Code

```dockerfile
COPY . .
```

Copies the files from the build context into the `/app` directory.

### 4. Install Dependencies

```dockerfile
RUN pip install -r requirements.txt
```

Installs the Python packages listed in `requirements.txt`.

### 5. Build the Application

```dockerfile
RUN python.py build
```

This is an example of a build command, but `python.py build` is not a standard Python command. Replace it with the actual build command supported by your application.

For example, if your build process generates a `dist` directory, the output might look like this:

```text
/app
└── dist/
```

At this point, the builder stage is complete.

---

## 🔹 Stage 2 — Runner Stage

The second stage contains the files and tools required to run the application.

### 1. Bring the Node.js Alpine Image

```dockerfile
FROM node:24-alpine AS runner
```

* `node:24-alpine` provides Node.js in a lightweight Alpine Linux image.
* `AS runner` names the second stage `runner`.

**Important:** This stage is suitable for a Node.js frontend only if the build output is compatible with the Node.js runtime or is served by a suitable web server.

### 2. Set the Working Directory

```dockerfile
WORKDIR /app
```

Sets `/app` as the working directory.

### 3. Copy `package.json`

```dockerfile
COPY package.json .
```

Copies `package.json` into `/app`.

### 4. Install Vite

```dockerfile
RUN npm install -g vite
```

Installs Vite globally inside the image.

### 5. Copy Build Files from the Builder Stage

```dockerfile
COPY --from=builder /app/dist ./dist
```

Copies the `dist` directory from the `builder` stage into `/app/dist` in the `runner` stage.

The `--from=builder` option tells Docker to copy files from the earlier stage named `builder`.

---

## 📄 Complete Multi-Stage Dockerfile

Save this example as `Dockerfile.multistage`.

**Note:** This illustrates the two-stage concept. A Python build stage followed by a Node.js runtime stage works only when the application and build output are compatible with that setup. The build command and startup configuration must match your actual project.

```dockerfile
# -------------------------------
# Stage 1: Builder
# -------------------------------

FROM python:3.14 AS builder

# Set the working directory
WORKDIR /app

# Copy application files
COPY . .

# Install Python dependencies
RUN pip install -r requirements.txt

# Build the application
# Replace with your actual build command
RUN python.py build


# -------------------------------
# Stage 2: Runner
# -------------------------------

FROM node:24-alpine AS runner

# Set the working directory
WORKDIR /app

# Copy package.json
COPY package.json .

# Install Vite
RUN npm install -g vite

# Copy build output from the builder stage
COPY --from=builder /app/dist ./dist

# Start the application
CMD ["npm", "run", "dev", "--", "--host", "0.0.0.0", "--port", "5174"]
```

### ⚠️ Important Notes

* The `python.py build` command is a placeholder and must be replaced with a valid command.
* If you run `npm run dev`, the `package.json` must define a `dev` script and the required dependencies must be installed.
* For a production frontend, use a production web server such as Nginx to serve the generated `dist` files.
* If you use Vite's development server, install the project's Node.js dependencies and copy the required source files into the runtime stage.

---

## 🐳 Build the Docker Image

If your Dockerfile is named `Dockerfile.multistage`, run:

```bash
docker build -t devboard-frontend-multistage -f Dockerfile.multistage .
```

### Why Use `-f`?

The `-f` option tells Docker which Dockerfile to use.

For a file named `Dockerfile`, Docker uses it by default:

```bash
docker build -t devboard-frontend-multistage .
```

### Command Breakdown

| Command        | Meaning                                         |
| -------------- | ----------------------------------------------- |
| `docker build` | Builds a Docker image                           |
| `-t`           | Assigns a name or tag to the image              |
| `-f`           | Specifies the Dockerfile                        |
| `.`            | Sets the current directory as the build context |

---

## ▶️ Run the Container

```bash
docker run -d --name devboard-frontend -p 5174:5174 devboard-frontend-multistage
```

### Port Mapping

```text
5174:5174
  │    │
  │    └── Container port
  └─────── Host port
```

* **Host port:** The port on your computer.
* **Container port:** The port inside the container.
* `-p 5174:5174` maps host port `5174` to container port `5174`.
* The application must listen on the container port for the mapping to work.

Access the application at:

`http://localhost:5174`

---

## 🔄 Multi-Stage Build Flow

```text
        Application Code
               |
               v
    +------------------------+
    |    Stage 1: Builder    |
    |                        |
    |    python:3.14         |
    |                        |
    |    Copy source code    |
    |    Install packages    |
    |    Build application   |
    |                        |
    |    Output: /app/dist   |
    +-----------+------------+
                |
                | COPY --from=builder
                v
    +------------------------+
    |     Stage 2: Runner    |
    |                        |
    |    node:24-alpine      |
    |                        |
    |    Copy build output   |
    |    Install runtime    |
    |    Start application   |
    +-----------+------------+
                |
                v
         Container Port 5174
                |
                v
       http://localhost:5174
```

### Key Takeaway

**Builder stage = Build the application.**

**Runner stage = Run the application.**

A multi-stage build allows you to keep the final image smaller by copying only the required files from the builder stage.

---

# 💾 Docker Volumes

## What Is a Docker Volume?

A **Docker volume** is a storage mechanism used to persist data outside a container's writable layer.

If a container is deleted, the data stored in a separate Docker volume remains available until the volume itself is deleted.

## 🔹 How Does It Work?

1. A container runs an application.
2. The application writes data to a directory inside the container.
3. Docker mounts a volume at that directory.
4. The data is stored in the volume rather than only in the container's writable layer.
5. If the container is deleted, the volume and its data remain.
6. A new container can mount the same volume and access the existing data.

## 🔹 Example

Imagine a database container stores customer information.

If the container is deleted without a volume, data stored only in its writable layer can be lost.

If the database stores its data in a Docker volume, you can delete and recreate the container while keeping the volume and its data.

## 🔹 Docker Volume vs Container

| Component        | Purpose                                                 |
| ---------------- | ------------------------------------------------------- |
| Container        | Runs the application                                    |
| Volume           | Stores persistent data                                  |
| Mount            | Connects the volume to a directory inside the container |
| Data persistence | Keeps data available beyond the container's lifecycle   |

## 🔹 Docker Volume Commands

### 1. Create a Volume

```bash
docker volume create myvolume
```

Creates a Docker volume named `myvolume`.

### 2. Run a Container with the Volume

```bash
docker run -d --name mycontainer -v myvolume:/app/data nginx
```

**Command breakdown:**

* `docker run` — Creates and starts a container.
* `-d` — Runs the container in the background.
* `--name mycontainer` — Assigns a name to the container.
* `-v myvolume:/app/data` — Mounts `myvolume` at `/app/data` inside the container.
* `nginx` — Specifies the image to run.

### 3. Verify the Volume

```bash
docker volume ls
```

Lists the Docker volumes on your system.

### 4. Inspect the Volume

```bash
docker volume inspect myvolume
```

Displays information about the volume.

### 5. Delete the Container

```bash
docker rm -f mycontainer
```

Removes the container. The named volume `myvolume` remains.

### 6. Reuse the Same Volume

```bash
docker run -d --name newcontainer -v myvolume:/app/data nginx
```

The new container mounts the same volume and can access data previously stored there.

**Important:** The example demonstrates volume mounting. The Nginx image does not automatically save all its website files to `/app/data`; an application must write its persistent data to the mounted directory.

---

## 🔄 Docker Volume Flow

```text
       Docker Container
      +------------------+
      |                  |
      |   Application    |
      |                  |
      |   /app/data      |
      +--------+---------+
               |
               | Volume Mount
               v
      +------------------+
      |   myvolume       |
      |                  |
      |   Persistent     |
      |      Data        |
      +------------------+

      Delete Container
               |
               v
      Volume Data Remains
```

## 🧠 Remember

**Docker Volume = Persistent Storage**

* Containers run applications.
* Volumes store data independently of a container's lifecycle.
* Mounting a volume connects persistent storage to a directory inside the container.
* Deleting a container does not automatically delete a named volume.
* Deleting a volume can permanently remove its stored data.

---

# 📚 Quick Revision

| Concept                | Main Purpose                                                  |
| ---------------------- | ------------------------------------------------------------- |
| Multi-Stage Dockerfile | Separates building from running an application                |
| Docker Volume          | Persists data beyond a container's lifecycle                  |
| Docker Networking      | Enables communication between containers and other systems    |
| Docker Compose         | Defines and runs multi-container applications                 |
| Docker Model Runner    | Runs supported AI models locally using Docker                 |
| AI Models on Docker    | Packages AI-related services and dependencies into containers |

**Next step:** Learn Docker Networking, Docker Compose, and how to run AI models with Docker.
