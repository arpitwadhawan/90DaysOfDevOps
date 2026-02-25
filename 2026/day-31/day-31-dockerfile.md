FROM — Base Image
Defines the starting point of your image.
Every Docker image must begin with FROM.
It pulls an existing image from Docker Hub (if not present locally).
Think of it like:
“Start building my image on top of this OS/application.”
Example:
FROM ubuntu:22.04
You’re starting from Ubuntu.

RUN — Execute Commands During Build
RUN apt update && apt install -y curl
Executes commands at build time.
Creates a new image layer.
Used to install packages or configure the system.
Important: RUN happens when we do docker build not when we do docker run.

COPY — Copy Files Into Image
COPY index.html /usr/share/nginx/html/
Copies files from your host machine into the image.
Happens at build time.
The copied files become part of the image.
If you rebuild, it copies again.

WORKDIR — Set Working Directory
WORKDIR /app
Sets the default directory for future instructions.
Similar to running cd /app.
Affects RUN, CMD, ENTRYPOINT, COPY.
Example:
WORKDIR /app
COPY . .
Now files copy into /app.

EXPOSE — Document Port
EXPOSE 3000
Tells Docker that the container listens on port 3000.
Does NOT publish the port to your machine.
Used by:
docker run -P
Docker Compose
Documentation
It’s informational, not functional for host access.

CMD — Default Command
CMD ["npm", "start"]
Defines the default command when container starts.
Runs at container runtime, not build time.
Can be overridden in docker run.
Example:
docker run myimage node app.js
This overrides CMD.



CMD vs ENTRYPOINT — Core Difference
Feature	                                      CMD	                ENTRYPOINT
Purpose	                              Default command	          Main executable
Can be overridden easily?                	✅ Yes          	  ❌ Not easily
Intended use	                        Provide defaults    	  Define container behavior
Runs at	                              Container start         Container start

CMD Example
FROM ubuntu
CMD ["echo", "Hello World"]
Run:  docker run myimage
Output: Hello World
Now override it: docker run myimage echo Hi
Output:  Hi (CMD is easily overridden.)

ENTRYPOINT Example
FROM ubuntu
ENTRYPOINT ["echo", "Hello"]
Run:  docker run myimage World
Output:  Hello World
Here:  ENTRYPOINT = fixed
Anything after image name becomes arguments
If we try:  docker run myimage echo Hi
It becomes: Hello echo Hi
ENTRYPOINT does not get replaced — arguments get appended.


Layer order matters because of Docker build cache.
Let’s break it clearly.How Docker Builds Images  :every Dockerfile instruction creates a layer:
FROM node:18        ← Layer 1
WORKDIR /app        ← Layer 2
COPY package.json . ← Layer 3
RUN npm install     ← Layer 4
COPY . .            ← Layer 5

Each layer is cached.How Docker Cache Works :when we run:
docker build .
Docker checks: “Has this instruction changed?”
If NO → it reuses cached layer
If YES → it rebuilds that layer and all layers after it
Why Order Matters
Let’s see a BAD order:
COPY . .
RUN npm install
If we change even 1 file in your project:
COPY . . changes
Cache breaks
RUN npm install runs again
Slow build

Correct Optimized Order
COPY package.json .
RUN npm install
COPY . .
Now:
If you change app code → only last layer rebuilds
npm install stays cached
Build is much faster
**Golden Rule**
Put:
Rarely changing layers at top
Frequently changing layers at bottom
