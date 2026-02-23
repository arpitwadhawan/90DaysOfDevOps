**What is a container and why do we need them?**
A container is a lightweight, portable unit that packages an application with all its dependencies so it can run consistently across different environments. Containers solve dependency 
issues,improve scalability, and make deployment faster and more reliable.
In simple layman words, A container is a lightweight, portable unit that packages an application with everything it needs to run — including:
Application code
Runtime (e.g., Java, Python, Node)
System libraries
Dependencies
Configuration files
So the app runs the same way everywhere.We can think of a container like a sealed lunchbox no matter where we take it — school, office, park — the food inside stays the same.Similarly, 
a container ensures:“It works on my machine” → becomes → “It works everywhere.” A popular container platform is Docker. With Docker:
-> We build a container image
-> Run it anywhere (Laptop, Server, Cloud)
-> No dependency issues
We need containers because it solves “**It Works on My Machine**” problem. Without containers:
  Dev machine → Ubuntu
  Production → CentOS
  Different versions of Python
  Different libraries
  App breaks.
With containers:
  Same OS layer
  Same dependencies
  Same runtime
  Same behavior
It is lightweight compared to Virtual Machines as containers share the host OS kernel.

**Container vs Virtual Machine** 
**Virtual Machine**          **Container**
Has its own OS              Shares OS kernel
Needs hypervisor            Isolated process
Heavy                       Lightweight
                            Faster startup

Docker Architecture Explained (Client, Daemon, Images, Containers, Registry)
Docker uses a client-server architecture. The Docker client sends commands to the Docker daemon, which builds images and runs containers. Images are read-only templates used to 
create containers, and registries like Docker Hub store and distribute images.
At its core, Docker uses a client-server architecture. Think of it like a restaurant:
The Docker Client is the customer who places an order (e.g., “Run this container!”).
The Docker Daemon (server) is the chef who prepares the meal in the kitchen.
Docker Desktop is the friendly menu and waiter that bridges your desktop OS to the Docker environment.
**Docker Client**: The Docker Client is what we use to interact with Docker. When we type: docker build, docker run, docker pull we are using the client.
The client then sends commands to the Docker Daemon, can run on the same machine or remotely, communicates using REST API.Think of it as the **frontend/command interface**.
**Docker Daemon (dockerd)**: The Docker Daemon is the brain of Docker.It listens for Docker API requests, builds images, runs containers, manages networks, manages volumes.
It runs in the background as a service. Without the daemon → Docker won’t work.
**Docker Images**: An Image is a read-only template used to create containers.
It contains OS layer (usually minimal Linux),Application code, Dependencies, Libraries, Environment configuration. Images are built from a Dockerfile.Example:
FROM node:18 (base)
WORKDIR /app  
COPY . .  (copying files from source to destinantion)
RUN npm install
CMD ["npm", "start"]
We build it using:
docker build -t myapp .
We can say an Image = Blueprint and Container = Running instance of that blueprint.
**Docker Containers**: A Container is a running instance of an image. When we run: docker run myapp, Docker:
Takes the image
Creates a writable layer
Starts the application inside an isolated environment
Containers are lightweight, share host OS kernel, start in seconds and are isolated processes
**Docker Registry**: A Registry stores Docker images. Most common registry: Docker Hub. Other registries:AWS ECR,Azure Container Registry,Google Container Registry,Private company registry
When we run: docker pull nginx, Docker contacts Docker Hub, downloads the nginx image,stores it locally.

How Everything Works Together, Step-by-step flow:
We run a command → docker run nginx
Docker Client sends request to Daemon
Daemon checks local images
If not found → pulls from Registry
Creates container from image
Runs container
