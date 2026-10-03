# Docker Fundamentals

## 1. What is Docker?

**Docker** is a platform used to package and run applications in isolated environments called **containers**.

Docker helps package an application together with its required:

- Application code
- Runtime
- Libraries
- Dependencies
- System packages
- Configuration

This helps the application run consistently across different environments.

---

## 2. Why Do We Use Docker?

### Problem

Suppose a developer creates an application on a **Windows laptop** using **Python 3.9**.

The application requires some specific:

- Python version
- Libraries
- Dependencies
- System packages
- Configuration

The application works perfectly on the developer's machine because all the required things are available there.

The developer thinks:

> "If it works on my machine, it should work on my friend's/client's machine too."

But the client may have a completely different environment.

For example:

- Developer's OS: Windows
- Client's OS: Linux
- Developer's Python: 3.9
- Client's Python: 3.14
- Required libraries may not be installed on the client system.
- Required dependencies or configurations may be missing.

Because of these differences, the application may work on the developer's machine but fail on the client machine.

This is commonly known as the:

> **"It works on my machine" problem.**

---

## 3. How Does Docker Solve This Problem?

Docker helps us package an application together with its required environment and dependencies.

We can define things such as:

- Application code
- Required Python version
- Required libraries
- Dependencies
- System packages
- Configuration

We then create a **Docker Image** containing this setup.

From the Docker Image, we can create a **Docker Container** and run the application.

### Simple Flow

```text
Application Code
       +
Python Version
       +
Libraries
       +
Dependencies
       +
Configuration
       |
       v
  Docker Image
       |
       v
Docker Container
       |
       v
Running Application
```

---

# 4. Dockerfile

A **Dockerfile** is a text file that contains instructions for building a Docker Image.

It tells Docker what environment and dependencies are required by the application.

### Example

```dockerfile
FROM python:3.9

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

### Important Dockerfile Instructions

| Instruction | Purpose |
|---|---|
| `FROM` | Defines the base image |
| `WORKDIR` | Sets the working directory |
| `COPY` | Copies files into the image |
| `RUN` | Executes a command while building the image |
| `EXPOSE` | Documents the port used by the application |
| `CMD` | Defines the default command to run the application |

### Dockerfile Flow

```text
Dockerfile
    |
    | docker build
    v
Docker Image
```

---

# 5. Docker Image

A **Docker Image** is a blueprint/template used to create Docker Containers.

It contains the required components needed to run an application.

For example:

```text
Application Code
       +
Python 3.9
       +
Required Libraries
       +
Dependencies
       +
Configuration
       |
       v
Docker Image
```

Think of a Docker Image as a **blueprint**.

The image itself is not the running application. A container is created from the image.

```text
Docker Image
     |
     | docker run
     v
Docker Container
```

---

# 6. Docker Container

A **Docker Container** is a running instance of a Docker Image.

The application runs inside the container using the environment and dependencies defined by the image.

```text
Docker Image
     |
     v
Docker Container
     |
     v
Running Application
```

We can create multiple containers from the same image.

```text
             Docker Image
                  |
        +---------+---------+
        |         |         |
        v         v         v
   Container  Container  Container
       1          2          3
```

---

# 7. Docker Registry

A **Docker Registry** is a place where Docker Images are stored and distributed.

A popular public registry is **Docker Hub**.

The basic workflow is:

```text
Developer
    |
    v
Docker Image
    |
   Push
    |
    v
Docker Registry
    |
   Pull
    |
    v
Other Machine
    |
    v
Docker Container
    |
    v
Running Application
```

### Common Commands

Build an image:

```bash
docker build -t myapp .
```

Push an image to a registry:

```bash
docker push username/myapp
```

Pull an image from a registry:

```bash
docker pull username/myapp
```

Run a container:

```bash
docker run username/myapp
```

---

# 8. Important Docker Terms

| Term | Meaning |
|---|---|
| **Docker** | Platform used to build, package, and run applications in containers |
| **Dockerfile** | File containing instructions to build a Docker Image |
| **Docker Image** | Blueprint/template used to create containers |
| **Docker Container** | Running instance of a Docker Image |
| **Docker Registry** | Place where Docker Images are stored and distributed |

---

# 9. Complete Docker Flow

```text
                    Dockerfile
                        |
                        | docker build
                        v
                  Docker Image
                        |
                        | docker run
                        v
                 Docker Container
                        |
                        v
                Running Application
```

### With Docker Registry

```text
                    Dockerfile
                        |
                        v
                  Docker Image
                        |
                      Push
                        |
                        v
                Docker Registry
                        |
                      Pull
                        |
                        v
                  Other Machine
                        |
                        v
                 Docker Container
                        |
                        v
                Running Application
```

---

# 10. Easy Way to Remember

```text
Dockerfile  = Instructions / Recipe

Docker Image = Blueprint / Template

Docker Container = Running Instance

Docker Registry = Storage / Repository for Images
```

### One-Line Flow

> **Dockerfile → Build → Image → Run → Container → Application**

### With Registry

> **Dockerfile → Image → Push → Registry → Pull → Container → Application**

---

# 11. Main Idea

> **Docker helps solve the "It works on my machine" problem by packaging an application with its required dependencies and providing a consistent environment to run it.**
