
## Docker Fundamentals
-----------------------------

## 1. What is Docker?
      
## 2. Why Do We Use Docker?
      
3. How Does Docker Work?

## Docker – Why We Use It
##  Dockerfile
## docker image,
## docker container,
## docker registry
  # Docker Fundamentals
## Problem

Suppose a developer creates an application on a Windows laptop using **Python 3.9**.

The application requires some specific:

* Python version
* Libraries
* Dependencies
* System packages
* Permissions/configurations

The application works perfectly on the developer's machine because all the required things are available there.

The developer thinks:

> "If it works on my machine, it should work on my friend's/client's machine too."

But the client may have a completely different environment.

For example:

* Developer's OS: Windows
* Client's OS: Linux
* Developer's Python: 3.9
* Client's Python: 3.14
* Required libraries may not be installed on the client system.
* Required dependencies or configurations may be missing.

Because of these differences, the application may work on the developer's machine but fail on the client machine.

## How Docker Solves This Problem

Docker helps us package an application together with its required environment and dependencies.

Inside a Docker-based environment, we can specify things such as:

* Application code
* Required Python version
* Required libraries
* Dependencies
* System packages
* Configuration

We then create a **Docker Image** containing this setup.

### Docker Image

A Docker Image can be thought of as a **blueprint/template** for running the application.

From this image, we can create a **Docker Container**.

### Docker Container

A container is a **running instance of a Docker image**.

The application runs inside the container with the environment and dependencies defined by the image.

## Simple Example

```text
Developer Machine
       ↓
Python 3.9
       ↓
Required Libraries
       ↓
Application
       ↓
Docker Image
       ↓
Docker Container
       ↓
Client Machine
       ↓
Application Runs in the Container
```

## Important Terms

**Docker:**
A platform/tool used to package and run applications in containers.

**Docker Image:**
A blueprint/template containing the application and its required environment.

**Docker Container:**
A running instance created from a Docker image.

## Main Idea

> **Docker helps solve the "It works on my machine" problem by packaging an application with its required dependencies and providing a consistent environm**
