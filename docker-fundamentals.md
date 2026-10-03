
## Docker Fundamentals
-----------------------------

## 1. What is Docker?
      
## 2. Why Do We Use Docker?
      
##3. How Does Docker Work?

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

```text
Docker Container
│
├── Application
├── Python 3.9
├── Required Libraries
├── Required Dependencies
├── Configuration
└── Required Environment

## Important Terms
** Docker engine:**
Docker is an engine that runs containerd. It uses core container technology to create, manage, and run containers.
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
