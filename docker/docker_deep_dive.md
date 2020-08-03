# Docker Deep Dive

## Introduction to Docker

**What is Docker?**

- Docker:
  - Docker, Inc. the company
  - Docker, the container runtime and orchestration engine
  - Docker, the open-source project (Moby)

**The Company**

- Docker, Inc.:
  - Based in San Francisco
  - Founded by Solomon Hykes
  - Start as a PaaS provider called dotCloud
  - dotCloud leveraged Linux containers
  - Their internal tool used to manage containers was nick-named Docker
  - In 2013 dotCloud was rebranded as Docker

**The Runtime and Orchestration Engine**

- Most people are referring to the Docker Engine
  - Two main editions:
    - Enterprise Edition (EE)
    - Community Edition (CE)
  - Both are released quarterly:
    - CE is supported for 4 months
    - EE is supported for 12 months

**The Open-Source Project**

- Moby:
  - The upstream project of Docker
  - Breaks Docker down into more modular components
  - Code is available on GitHub: https://github.com/moby/moby

**Why Use Docker?**

- Docker Use Cases:
  - Dev/Prod parity:
    - Dev and Production environment are the same
    - Bugs in Production can be replicated in Development
  - Simplifying Configuration:
    - Lets you put your environment and configuration into code and deploy it
    - Allows the same Docker configuration to be used in a variety of environments
    - Decouples infrastructure requirements from the application environment
  - Code Pipeline Management:
    - Build standards and repeatable processes
  - Developer Productivity
  - App Isolation
  - Server Consolidation
  - Debugging Capabilities
  - Multi-tenancy

---

## Installing Docker

**Uninstall old versions:**

```sh
sudo yum remove -y docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

**Install Docker CE**

```sh
# Add the Utilities needed for Docker:
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2

# Set up the stable repository:
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

# Install Docker CE:
sudo yum -y install docker-ce

# Enable and start Docker:
sudo systemctl start docker && sudo systemctl enable docker

# Add cloud_user to the docker group:
sudo usermod -aG docker cloud_user
```

---

## Docker Under the Hood

### Architecture Overview

- Client-server architecture
- Client talks to the Docker daemon
- The Docker daemon handles:
  - Building
  - Running
  - Distributing
- Both communicate using a REST API:
  - UNIX sockets
  - Network interface

**The Docker daemon (dockerd)**:

- Listens for Docker API requests and manages Docker objects:
  - Images
  - Containers
  - Networks
  - Volumes

**The Docker client (docker)**:

- Is how users interact with Docker
- Sends commands to dockerd

**Docker registries:**

- Stores Docker images
- Public registry such as DockerHub
- Let you run your own private registry

**Docker objects:**

- Images:
  - Read-only template with instructions for - creating a Docker container
  - Image is based on another image
  - Create your own images
  - Use images published to a registry
  - Use a Dockerfile to build images
- Containers:
  - Runnable instance of an image
  - Connect a container to networks
  - Attach storage
  - Create a new image based on its current state
  - Isolated from other containers and the host machine
- Services
  - Scale containers across multiple Docker - daemons
  - Docker Swarm
  - Define the desired state
  - Service is load-balanced

**Docker Swarm:**

- Multiple Docker daemons (Master and Workers)
- The daemons all communicate using the Docker API
- Supported in Docker 1.12 and higher

---

### The Docker Engine

- Modular in design:
  - Batteries included but replaceable
- Based on open-standards outline by the Open Container Initiative
- The major components:
  - Docker client
  - Docker daemon
  - containerd
  - runc
- The components work together to create and run containers

**A Brief History of the Docker Engine**

- The first release of Docker:
  - The Docker daemon:
  - Monolithic binary
  - Docker client
  - Docker API
  - Container runtime
  - Image builds
  - Much more...
- LXC:
  - Namespaces
  - Control groups (cgroups)
  - Linux-specific

**Refactoring of the Docker Engine**

- LXC was later replaced with libcontainer:
  - Docker 0.9
  - Platform agnostic
  - Issues with the monolithic Docker daemon:
- Harder to innovate
  - Slow
  - Not what the ecosystem wanted
- Docker became more modular:
  - Smaller more specialized tools
  - Pluggable architecture
- Open Container Initiative:
  - Image spec
  - Container runtime spec
  - Version 1.0 release in 2017
  - Docker Inc. heavily contributed
  - Docker 1.11 (2016) used the specification as much as possible
- runc:
  - Implemenation of the OCI container-runtime-spec
  - Lightweght CLI wrapper for libcontainer
  - Create containers
- containerd:
  - Manages container lifecycle
    - Start
    - Stop
    - Pause
    - Delete
  - Image management
  - Part of the 1.11 release
- shim:
  - Implemenation of daemonless Containers
  - containerd forks an instance of runc for each - new container
  - runc process exits after the container is created
  - shim process becomes the container parent
  - Responsible for:
    - STDIN and STDOUT
    - Reporting exit status to the Docker daemon

---

### Running Containers

`docker container run -it --name <NAME> <IMAGE>:<TAG>`

- Creating a container:
  - CLI use for executing a command
  - Docker client uses the appropriate API payload
  - POSTs to the correct API endpoint
  - Docker deamon receives instructions
  - Docker deamon calls containerd to start a new container
  - Docker daemon uses gRPC (a CRUD style API)
  - containerd creates an OCI bundle from the Docker image
  - Tells runc to create a container using the OCI bundle
  - runc interfaces with the OS kernal to get the constructs needed to create a container
    - This includes namespaces, cgroups, etc.
  - Container process starts as a child process
  - runc exits once the container starts
  - Process is complete, and container is running

---

### Docker Images and Containers

- What are Docker images?
  - Files comprised of multiple layers
  - Execute code in a Docker container
  - Built from the instructions
  - Use images to create an instance of a container
- Docker images and layers
  - Image are made of multiple layers.
  - Each layer represents an instruction in the - image’s Dockerfile.
  - Each layer except, the very last one, is read-only.
  - Each layer is only a set of differences from the layer before it.
  - Layers are stacked on top of each other.
  - Containers add new writable layers on top of the underlying layers
  - All changes made to a running container is made to the Container layer
- What are containers?
  - A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another.
- Container and layers
  - Top writable layer
  - All changes are stored in the writable layer
  - The writable layer is deleted when the container is deleted
  - The image remains unchanged

---

### Docker Hub

- Public Docker registry
- Provided by Docker
  - Features:
    - Repositories
    - Teams and Organizations
    - Official Images
    - Publisher Images
    - Builds
    - Webhooks
- https://hub.docker.com/signup

---

## Docker Basics

### Docker commands

Get a list of all of the Docker commands:

`docker -h`

- Management Commands:
  - `builder` Manage builds
  - `config` Manage Docker configs
  - `container` Manage containers
  - `engine` Manage the docker engine
  - `image` Manage images
  - `network` Manage networks
  - `node` Manage Swarm nodes
  - `plugin` Manage plugins
  - `secret` Manage Docker secrets
  - `service` Manage services
  - `stack` Manage Docker stacks
  - `swarm` Manage Swarm
  - `system` Manage Docker
  - `trust` Manage trust on Docker images
  - `volume` Manage volumes
- docker image:
  - `build` Build an image from a dockerfile
  - `history` Show the history of an image
  - `import` Import the contents from a tarball to create a filesystem image
  - `inspect` Display detailed information on one or more images
  - `load` Load an image from a tar file or STDIN
  - `ls` List images
  - `prune` Remove unused images
  - `pull` Pull an image or a repository from a registry
  - `push` Push an image or a repository to a registry
  - `rm` Remove one or more images
  - `save` Save one or more images to a tar file (streamed to STDOUT by default)
  - `tag` Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
- docker container:
  - `attach` Attach local standard input, output, and error streams to a running container
  - `commit` Create a new image from a container's changes
  - `cp` Copy files/folders between a container and the local filesystem
  - `create` Create a new container
  - `diff` Inspect changes to files or directories on a container's filesystem
  - `exec` Run a command in a running container
  - `export` Export a container's filesystem as a tar archive
  - `inspect` Display detailed information on one or more containers
  - `kill` Kill one or more running containers
  - `logs` Fetch the logs of a container
  - `ls` List containers
  - `pause` Pause all processes within one or more containers
  - `port` List port mappings or a specific mapping for the container
  - `prune` Remove all stopped containers
  - `rename` Rename a container
  - `restart` Restart one or more containers
  - `rm` Remove one or more containers
  - `run` Run a command in a new container
  - `start` Start one or more stopped containers
  - `stats` Display a live stream of container(s) resource usage statistics
  - `stop` Stop one or more running containers
  - `top` Display the running processes of a container
  - `unpause` Unpause all processes within one or more containers
  - `update` Update configuration of one or more containers
  - `wait` Block until one or more containers stop, then print their exit codes

```
# list containers
docker container ls

# start container
docker container start <id>

# stop container
docker container stop <id>

# see stats
docker container stats <id>

# exec, -i: interactive, -t: tty
docker container exec -it <id> /bin/bash
docker container exec -it <id> ls /usr/share/nginx/html/

# pause container
docker container pause <id>

# clean up, use -f on running instances
docker container rm <id>

# remove all stopped containers
docker container prune
```

---

### Creating Containers

- `docker container run:`
  - `--help` Print usage
  - `--rm` Automatically remove the container when it exits
  - `-d, --detach` Run container in background and print container ID
  - `-i, --interactive` Keep STDIN open even if not attached
  - `--name` string Assign a name to the container
  - `-p, --publish` list Publish a container's port(s) to the host
  - `-t, --tty` Allocate a pseudo-TTY
  - `-v, --volume` list Mount a volume (the bind type of mount)
  - `--mount` mount Attach a filesystem mount to the container
  - `--network` string Connect a container to a network (default "default")
- Create a container and attach to it:
  `docker container run –it busybox`
- Create a container and run it in the background:
  `docker container run –d nginx`
- Create a container that you name and run it in the background:
  `docker container run –d –name myContainer busybox`

---

### Exposing and Publishing Container Ports

- Exposing:
  - Expose a port or a range of ports
  - This does not publish the port
  - Use `--expose [PORT]`

`docker container run --expose 1234 [IMAGE]`

- Publishing:
  - Maps a container's port to a host`s port
  - `-p or --publish` publishes a container's port(s) to the host
  - `-P, or --publish-all` publishes all exposed ports to random ports

```
docker container run -p [HOST_PORT]:[CONTAINER_PORT] [IMAGE]
docker container run -p [HOST_PORT]:[CONTAINER_PORT]/tcp -p [HOST_PORT]:[CONTAINER_PORT]/udp [IMAGE]
docker container run -P
```

- Lists all port mappings or a specific mapping for a container:

`docker container port [Container_NAME]`

---

### Executing Container Commands

- Executing a command:
  - Dockerfile
  - During a Docker run
  - Using the exec command
- Commands can be:
  - One and done Commands
  - Long running Commands
- Start a container with a command:

`docker container run [IMAGE][cmd]`

- Execute a command on a container:

`docker container exec -it [NAME][cmd]`

- Example:

```
docker container run -d -p 8080:80 nginx
docker container ps
docker container exec -it [NAME] /bin/bash
docker container exec -it [NAME] ls /usr/share/nginx/html/
```

---

### Container Logging

- Create a container using the weather-app image.

`docker container run --name weather-app -d -p 80:3000 linuxacademycontent/weather-app`

- Show information logged by a running container:

`docker container logs [NAME]`

- Show information logged by all containers participating in a service:

`docker service logs [SERVICE]`

- Logs need to be output to STDOUT and STDERR.
- Nginx Example:

```
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log
```

- Debug a failed container deploy:

```
docker container run -d --name ghost_blog \
-e database__client=mysql \
-e database__connection__host=mysql \
-e database__connection__user=root \
-e database__connection__password=P4sSw0rd0! \
-e database__connection__database=ghost \
-p 8080:2368 \
ghost:1-alpine
```

---

## Networking

### Networking Overview

- Docker Networking:
  - Open-source pluggable architecture
  - Container Network Model (CNM)
  - libnetwork implements CNM
  - Drivers extend the network topologies
- Network Drivers:
  - bridge
  - host
  - overlay
  - macvlan
  - none
  - Network plugins
- Container Network Model
  - Defines three building blocks:
    - Sandboxes
    - Endpoints
    - Networks

---

### Networking Commands

**Networking Basics**

`ifconfig`

- List all Docker network commands:

`docker network -h`

- Command Summary:

  - `connect` - Connect a container to a network
  - `create` - Create a network
  - `disconnect` - Disconnect a container from a network
  - `inspect` - Display detailed information on one or more networks
  - `ls` - List networks
  - `prune` - Remove all unused networks
  - `rm` - Remove one or more networks

- List all Docker networks on the host:

```
docker network ls
docker network ls --no-trunc
```

- Getting detailed info on a network:

`docker network inspect [NAME]`

- Creating a network:

`docker network create br00`

- Deleting a network:

`docker network rm [NAME]`

- Remove all unused networks:

`docker network prune`

**Adding and Removing containers to a network**

- Create a container with no network:

`docker container run -d --name network-test03 -p 8081:80 nginx`

- Create a new network:

`docker network create br01`

- Add the container to the bridge network:

`docker network connect br01 network-test03`

- Inspect network-test03 to see the networks:

`docker container inspect network-test03`

- Remove network-test03 from br01:

`docker network disconnect br01 network-test03`

---

### Networking Containers

**Creating a network and defining a Subnet and Gateway**

- Create a bridge network with a subnet and gateway:

```
docker network create --subnet 10.1.0.0/24 --gateway 10.1.0.1 br02
```

- Run ifconfig to view the bridge interface for br02:

`ifconfig`

- Inspect the br02 network:

`docker network inspect br02`

- Prune all unused networks:

`docker network prune`

- Create a network with an IP range:

```
docker network create --subnet 10.1.0.0/16 --gateway 10.1.0.1 --ip-range=10.1.4.0/24 --driver=bridge --label=host4network br04
```

- Inspect the br04 network:

`docker network inspect br04`

- Create a container using the br04 network:

```
docker container run --name network-test01 -it --network br04 centos /bin/bash
```

- Install Net Tools:

```
yum update -y
yum install -y net-tools
```

- Get the IP info for the container:

`ifconfig`

- Get the gateway info the container:

`netstat -rn`

- Get the DNS info for the container:

`cat /etc/resolv.conf`

**Assigning IPs to a container:**

- Create a new container and assign an IP to it:

```
docker container run -d --name network-test02 --ip 10.1.4.102 --network br04 nginx
```

- Get the IP info for the container:

`docker container inspect network-test02 | grep IPAddr`

- Inspect network-test03 to see that br01 was removed:

`docker container inspect network-test04`

**Networking two containers**

- Create an internal network:

```
docker network create -d bridge --internal localhost
```

- Create a MySQL container that is connected to localhost:

```
docker container run -d --name test_mysql -e MYSQL_ROOT_PASSWORD=P4sSw0rd0 --network localhost mysql:5.7
```

- Create a container that can ping the MySQL container:

```
docker container run -it --name ping-mysql --network bridge centos
```

- Connect ping-mysql to the localhost network:

`docker network connect localhost ping-mysql`

- Restart and attach to container:

`docker container start -ia ping-mysql`

Create a container that can't ping the MySQL container:

```
docker container run -it --name cant-ping-mysql centos
```

- Create a Nginx container that is not publicly accessible:

```
docker container run -d --name private-nginx -p 8081:80 --network localhost nginx
```

- Inspect private-nginx:

`docker container inspect private-nginx`

---

## Storage

### Storage Overview

- Categories of data storage:
  - Non-persistent:
    - Local storage
    - Data that is ephemeral
    - Every container has it
    - Tied to the lifecycle of the contain
  - Persistent
    - Volumes
    - Volumes are decoupled from containers

**Non-persistent Data**

- By default all container use local storage
- Storage locations:
  - Linux: `/var/lib/docker/[STORAGE-DRIVER]/`
  - Windows: `C:\ProgramData\Docker\windowsfilter\`
- Storage Drivers:
  - RHEL uses overlay2.
  - Ubuntu uses overlay2 or aufs.
  - SUSE uses btrfs.
  - Windows uses its own.

**Persistent Data Using Volumes**

- Use a volume for persistent data:
  - Create the volume first, then create your container.
- Mounted to a directory in the container
- Data is written to the volume
- Deleting a container does not delete the volume
- First-class citizens
- Uses the local driver
- Third party drivers:
  - Block storage
  - File storage
  - Object storage
- Storage locations:
  - Linux: /var/lib/docker/volumes/
  - Windows: C:\ProgramData\Docker\volumes

---

### Volume Commands

- List all Docker volume commands:

`docker volume -h`

- List all volumes on a host:

`docker volume ls`

- Create two new volumes:

```
docker volume create test-volume1
docker volume create test-volume2
```

- Get the flags available when creating a volume:

`docker volume create -h`

- Inspecting a volume:

`docker volume inspect test-volume1`

- Deleting a volume:

`docker volume rm test-volume`

- Removing all unused volumes:

`docker volume prune`

---

### Using Bind Mounts

- Bind mounts have been around since the early days of Docker. They have limited functionality compared to volumes. With bind mount, a file or directory on the host machine is mounted into a container.
- Volumes use a new directory that is created within Docker’s storage directory on the host machine, and Docker manages that directory’s contents.
- Using the mount flag:

```
mkdir target

docker container run -d \
  --name nginx-bind-mount1 \
  --mount type=bind,source="$(pwd)"/target,target=/app \
  nginx
docker container ls
```

- Bind mounts won't show up when listing volumes:
  `docker volume ls`
- Inspect the container to find the bind mount:
  `docker container inspect nginx-bind-mount1`
- Create a new file in /app on the container:

```
docker container exec -it nginx-bind-mount1 /bin/bash
cd target
touch file1.txt
ls
exit
```

- Using the volume flag:

```
docker container run -d \
 --name nginx-bind-mount2 \
 -v "$(pwd)"/target2:/app \
 nginx
```

- Create /app/file3.txt in the container:

```
docker container exec -it nginx-bind-mount2 touch /app/file3.txt
ls target2
```

- Create an nginx.conf file:

```
mkdir nginx
cat << EOF >  nginx/nginx.conf
user  nginx;
worker_processes  1;

error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}
EOF
```

- Create an Nginx container that creates a bind mount to nginx.conf:

```
docker container run -d \
 --name nginx-bind-mount3 \
 -v "$(pwd)"/nginx/nginx.conf:/etc/nginx/nginx.conf \
 nginx
```

- Look at the bind mount by inspecting the container:

`docker container inspect nginx-bind-mount3`

---

### Using Volumes for Persistent Storage

- Volumes are the preferred method for maintaining persistent data.
- Volumes are easier to back up or migrate than bind mounts.
- You can manage volumes using Docker CLI commands or the Docker API.
- They work on both Linux and Windows containers.
- Volumes can be more safely shared among **multiple** containers.
- Volume drivers allow for:

  - Storing volumes on remote hosts or cloud providers
  - Encrypting the contents of volumes
  - Add other functionality

- New volumes can have their content pre-populated by a container.

- Create a new volume for an Nginx container:

`docker volume create html-volume`

- Creating a volume using that volume mount:

```
docker container run -d \
 --name nginx-volume1 \
 --mount type=volume,source=html-volume,target=/usr/share/nginx/html/ \
 nginx
```

- Inspect the volume:

`docker volume inspect html-volume`

- List the contents of html-volume:

`sudo ls /var/lib/docker/volumes/html-volume/_data`

- Creating a volume using that volume flag:

```
docker container run -d \
 --name nginx-volume2 \
 -v html-volume:/usr/share/nginx/html/ \
 nginx
```

- Edit index.html:

`sudo vi /var/lib/docker/volumes/html-volume/_data/index.html`

- Inspect nginx-volume2 to get the private IP:

`docker container inspect nginx-volume2`

- Login into nginx-volume1 and go to the html directory:

```
docker container exec -it nginx-volume3 /bin/bash
cd /usr/share/nginx/html
cat index.hml
```

- Install Vim:

```
apt-get update -y
apt-get install vim -y
```

## Dockerfile

### Introduction

- Dockerfiles are instructions. They contains all of the commands used to build an image.
  - Docker images consist of read-only layers.
  - Each represents a Dockerfile instruction.
  - Layers are stacked.
  - Each layer is a result of the changes from the previous layer.
  - Images are built using the docker image build command.

**Dockerfile Layers**

```
Dockerfile:
FROM ubuntu:15.04
COPY . /app
RUN make /app
CMD python /app/app.py
```

- FROM creates a layer from the ubuntu:15.04 Docker image.
- COPY adds files from your Docker client’s current directory.
- RUN builds your application with make.
- CMD specifies what command to run within the container.

**Best Practices**

- Keep containers as ephemeral as possible.
- Follow Principle 6 of the 12 Factor App.
- Avoid including unnecessary files.
- Use .dockerignore.
- Use multi-stage builds.
- Don’t install unnecessary packages.
- Decouple applications.
- Minimize the number of layers.
- Sort multi-line arguments.
- Leverage build cache.

---

### Working with Instructions

- FROM: Initializes a new build stage and sets the Base Image
- RUN: Will execute any commands in a new layer
- CMD: Provides a default for an executing container. There can only be one CMD instruction in a Dockerfile
- LABEL: Adds metadata to an image
- EXPOSE: Informs Docker that the container listens on the specified network ports at runtime
- ENV: Sets the environment variable <key> to the value <value>
- ADD: Copies new files, directories or remote file URLs from <src> and adds them to the filesystem of the image at the path <dest>.
- COPY: Copies new files or directories from <src> and adds them to the filesystem of the container at the path <dest>.
- ENTRYPOINT: Allows for configuring a container that will run as an executable
- VOLUME: Creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers
- USER: Sets the user name (or UID) and optionally the user group (or GID) to use when running the image and for any RUN, CMD, and ENTRYPOINT instructions that follow it in the Dockerfile
- WORKDIR: Sets the working directory for any RUN, CMD, ENTRYPOINT, COPY, and ADD instructions that follow it in the Dockerfile
- ARG: Defines a variable that users can pass at build-time to the builder with the docker build command, using the --build-arg <varname>=<value> flag
- ONBUILD: Adds a trigger instruction to the image that will be executed at a later time, when the image is used as the base for another build
- HEALTHCHECK: Tells Docker how to test a container to check that it is still working
- SHELL: Allows the default shell used for the shell form of commands to be overridden

- To set up the environment:

```sh
sudo yum install git -y
mkdir docker_images
cd docker_images
mkdir weather-app
cd weather-app
git clone https://github.com/linuxacademy/content-weather-app.git src
```

- Create the Dockerfile:

```sh
vi Dockerfile
```

- Dockerfile contents:

```docker
# Create an image for the weather-app

FROM node
LABEL org.label-schema.version=v1.1
RUN mkdir -p /var/node
ADD src/ /var/node/
WORKDIR /var/node
RUN npm install
EXPOSE 3000
CMD ./bin/www
```

- Build the weather-app image:

```
docker image build -t linuxacademy/weather-app:v1 .
```

- List the images:

```
docker image ls
```

- Create the weather-app container:

```
docker container run -d --name weather-app1 -p 8081:3000 linuxacademy/weather-app:v1
```

- List all running containers:

```
docker container ls
```

---

### Environment Variables

- To make new software easier to run, you can use ENV to update the PATH environment variable for the software that your container installs.
- Setup your environment:

```sh
cd docker_images
mkdir env
cd env
```

- Use the --env flag to pass an environment variable when building an image:

```
--env [KEY]=[VALUE]
```

- Use the ENV instruction in the Dockerfile:

```
ENV [KEY]=[VALUE]
ENV [KEY][value]
```

- Clone the weather-app:

```sh
git clone https://github.com/linuxacademy/content-weather-app.git src
```

- Create the Dockerfile

```sh
vi Dockerfile
```

- Dockerfile contents:

```docker
# Create an image for the weather-app

FROM node
LABEL org.label-schema.version=v1.1
ENV NODE_ENV="development"
ENV PORT 3000

RUN mkdir -p /var/node
ADD src/ /var/node/
WORKDIR /var/node
RUN npm install
EXPOSE \$PORT
CMD ./bin/www
```

- Create the weather-app container:

```
docker image build -t linuxacademy/weather-app:v2 .
```

- Inspect the container to see the environment variables:

```
docker image inspect linuxacademy/weather-app:v2
```

- Deploy the weather-dev application:

```
docker container run -d --name weather-dev -p 8082:3001 --env PORT=3001 linuxacademy/weather-app:v2
```

- Inspect the development container to see the environment variables:

```
docker container inspect weather-dev
```

- Deploy the weather-app to production:

```
docker container run -d --name weather-app2 -p 8083:3001 --env PORT=3001 --env NODE_ENV=production linuxacademy/weather-app:v2
```

- Inspect the production container to see the environment variables:

```
docker container inspect weather-app2
```

- Get the logs for weather-app2:

```
docker container logs weather-app2
docker container run -d --name weather-prod -p 8084:3000 --env NODE_ENV=production linuxacademy/weather-app:v2
```

---

### Build Arguments

- Use the --build-arg flag when building an image:

```
--build-arg [NAME]=[VALUE]
```

- Use the ARG instruction in the Dockerfile:

```
ARG [NAME]=[DEFAULT_VALUE]
```

- Navigate to the args directory:

```sh
cd docker_images
mkdir args
cd args
```

- Clone the weather-app:

```sh
git clone https://github.com/linuxacademy/content-weather-app.git src
```

- Create the Dockerfile:

```sh
vi Dockerfile
```

```docker
Dockerfile:

# Create an image for the weather-app
FROM node
LABEL org.label-schema.version=v1.1
ARG SRC_DIR=/var/node
RUN mkdir -p $SRC_DIR
ADD src/ $SRC_DIR
WORKDIR $SRC_DIR
RUN npm install
EXPOSE 3000
CMD ./bin/www
```

- Create the weather-app container:

```
docker image build -t linuxacademy/weather-app:v3 --build-arg SRC_DIR=/var/code .
```

- Inspect the image:

```
docker image inspect linuxacademy/weather-app:v3 | grep WorkingDir
```

- Create the weather-app container:

```
docker container run -d --name weather-app3 -p 8085:3000 linuxacademy/weather-app:v3
```

- Verify that the container is working by executing curl:

```
curl localhost:8085
```

### Working with Non-privileged Users

- Rather than using root, we can use a non-privileged user to configure and run an application.
- Setup your environment:

```sh
cd docker_images
mkdir non-privileged-user
cd non-privileged-user
```

- Create the Dockerfile:

```
vi Dockerfile
```

```docker
Dockerfile contents:

# Creates a CentOS image that uses cloud_user as a non-privileged user
FROM centos:latest
RUN useradd -ms /bin/bash cloud_user
USER cloud_user
```

- Build the new image:

```
docker image build -t centos7/nonroot:v1 .
```

- Create a container using the new image:

```
docker container run -it --name test-build centos7/nonroot:v1 /bin/bash
```

- Connecting as a privileged user:

```
docker container start test-build
docker container exec -u 0 -it test-build /bin/bash
```

- Set up the environment:

```
cd ~/docker_images
mkdir node-non-privileged-user
cd node-non-privileged-user
```

- Create the Dockerfile:

```
vi Dockerfile
```

```docker
Dockerfile contents:

# Create an image for the weather-app
FROM node
LABEL org.label-schema.version=v1.1
RUN useradd -ms /bin/bash node_user
USER node_user
ADD src/ /home/node_user
WORKDIR /home/node_user
RUN npm install
EXPOSE 3000
CMD ./bin/www
git clone https://github.com/linuxacademy/content-weather-app.git src
```

- Build the weather-app image using the non-privileged user node_user:

```
docker image build -t linuxacademy/weather-app-nonroot:v1 .
```

- Create a container using the linuxacademy/weather-app-nonroot:v1 image:

```
docker container run -d --name weather-app-nonroot -p 8086:3000 linuxacademy/weather-app-nonroot:v1
```

---

### Order of Execution

- Some instructions may have unintended consequences that can cause your build to fail.
- Setup your environment:

```
cd docker_images
mkdir centos-conf
cd centos-conf
```

- Create the Dockerfile:

```sh
vi Dockerfile
```

```docker
Dockerfile contents:

# Creates a CentOS image that uses cloud_user as a non-privileged user
FROM centos:latest
RUN mkdir -p ~/new-dir1
RUN useradd -ms /bin/bash cloud_user
USER cloud_user
RUN mkdir -p ~/new-dir2
RUN mkdir -p /etc/myconf
RUN echo "Some config data" >> /etc/myconf/my.conf
```

- Build the new image:

```
docker image build -t centos7/myconf:v1 .
```

### Using the Volume Instruction

- Use the VOLUME instruction to automatically create a mount point in a Docker image. When a container is created using this image, a volume will be created and mounted to the specified directory.
- Set up your environment:

```
cd docker_images
mkdir volumes
cd volumes
```

- Create the Dockerfile:

```
vi Dockerfile
```

- Build an Nginx image that uses a volume:

```
FROM nginx:latest
VOLUME ["/usr/share/nginx/html/"]
```

- Build the new image:

```
docker image build -t linuxacademy/nginx:v1 .
```

- Create a new container using the linuxacademy/nginx:v1 image:

```
docker container run -d --name nginx-volume linuxacademy/nginx:v1
```

- Inspect nginx-volume:

```
docker container inspect nginx-volume
```

- List the volumes:

```
docker volume ls | grep [VOLUME_NAME]
```

- Inspect the volumes:

```
docker volume inspect [VOLUME_NAME]
```

---

### Entrypoint vs. Command

- Though ENTRYPOINT functions very similarly to CMD it's behaviors are very different.
- ENTRYPOINT allows us to configure a container that will run as an executable.
- We can override all elements specified using CMD.
- Using the docker run --entrypoint flag will override the ENTRYPOINT instruction.
- Setup your environment:

```
cd docker_images
mkdir entrypoint
cd entrypoint
```

- Create the Dockerfile:

```sh
vi Dockerfile
```

```docker
Dockerfile contents:

# Create an image for the weather-app
FROM node
LABEL org.label-schema.version=v1.1
ENV NODE_ENV="production"
ENV PORT 3001
RUN mkdir -p /var/node
ADD src/ /var/node/
WORKDIR /var/node
RUN npm install
EXPOSE $PORT
ENTRYPOINT ./bin/www
```

- Clone the image:

```
git clone https://github.com/linuxacademy/content-weather-app.git src
```

- Build the image:

```
docker image build -t linuxacademy/weather-app:v4 .
```

- Deploy the weather-app:

```
docker container run -d --name weather-app4 linuxacademy/weather-app:v4
```

- Inspect weather-app4:

```
docker container inspect weather-app4 | grep Cmd
docker container inspect weather-app-nonroot
docker container inspect weather-app4
```

- Create the weather-app container:

```
docker container run -d --name weather-app5 -p 8083:3001 linuxacademy/weather-app:v4 echo "Hello World"
```

- Inspect weather-app5:

```
docker container inspect weather-app5
```

- Create the volumes for Prometheus:

```
docker volume create prometheus
docker volume create prometheus_data

sudo chown -R nfsnobody:nfsnobody /var/lib/docker/volumes/prometheus/
sudo chown -R nfsnobody:nfsnobody /var/lib/docker/volumes/prometheus_data/
```

- Create the Prometheus container:

```
docker run --name prometheus -d -p 8084:9090 \
  -v prometheus:/etc/prometheus \
  -v prometheus_data:/prometheus/data \
  prom/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path=/prometheus/data
```

- Inspect Prometheus:

```
docker container inspect prometheus
```

---

### Using .dockerignore

- Setup your environment:

```sh
cd docker_images
mkdir dockerignore
cd dockerignore
git clone https://github.com/linuxacademy/content-weather-app.git src
cd src
git checkout dockerignore
cd ../
```

- Create the .dockerignore file:

```sh
vi .dockerignore
```

- Add the following to .dockerignore:

```
# Ignore these files
*/*.md
*/.git
src/docs/
*/tests/
```

- Create the Dockerfile:

```sh
vi Dockerfile
```

```docker
Dockerfile contents:

# Create an image for the weather-app
FROM node
LABEL org.label-schema.version=v1.1
ENV NODE_ENV="production"
ENV PORT 3000
RUN mkdir -p /var/node
ADD src/ /var/node/
WORKDIR /var/node
RUN npm install
EXPOSE $PORT
ENTRYPOINT ["./bin/www"]
```

- Build the image:

```
docker image build -t linuxacademy/weather-app:v5 .
```

- Create the weather-app container:

```
docker container run -d --name weather-app-ignore linuxacademy/weather-app:v5
```

- List the contents of /var/node:

```
docker container exec weather-app-ignore ls -la /var/node
```

---

## Building and Distributing Images

### Building Images

- To build one:

```docker
docker image build -t <NAME>:<TAG> .
```

- Useful flags:
  - `-f, --file string`: This is the name of the Dockerfile (Default is PATH/Dockerfile).
  - `--force-rm`: Always remove intermediate containers.
  - `--label list`: Set metadata for an image.
  - `--rm`: Remove intermediate containers after a successful build (default is true).
  - `--ulimit ulimit`: This sets ulimit options (default is []).

```
cd docker_images/weather-app
cp Dockerfile Dockerfile.test
docker image build -t linuxacademy/weather-app:path-example1 -f Dockerfile.test .
docker image build -t linuxacademy/weather-app:path-example2 --label com.linuxacademy.version=v1.8 -f Dockerfile.test .
```

- Building image by piping the Dockerfile through STDIN:

```
docker image build -t <NAME>:<TAG> -<<EOF
Build instructions
EOF
```

- Example:

```
docker image build -t linuxacademy/nginx:stind --rm -<<EOF
FROM nginx:latest
VOLUME ["/usr/share/nginx/html/"]
EOF
```

- Building an image using a URL:

```
docker image build -t <NAME>:<TAG> <GIT_URL>#<REF>
docker image build -t <NAME>:<TAG> <GIT_URL>#:<DIRECTORY>
docker image build -t <NAME>:<TAG> <GIT_URL>#<REF>:<DIRECTORY>
```

- Example:

```
docker image build -t linuxacademy/weather-app:github https://github.com/linuxacademy/content-weather-app.git#remote-build
```

- Building an image from a zip file:

```
docker image build -t <NAME>:<TAG> - < <FILE>.tar.gz
```

- Example:

```
cd docker_images
mkdir tar_image
cd tar_image
git clone https://github.com/linuxacademy/content-weather-app.git
cd content-weather-app
git checkout remote-build
tar -zcvf weather-app.tar.gz Dockerfile src
docker image build -t linuxacademy/weather-app:from-tar - < weather-app.tar.gz
```

---

### Using Multi-Stage Builds

- By default, the stages are not named
  - Stages are numbered with integers
  - Starting with 0 for the first FROM instruction
  - Name the stage by adding as to the FROM instruction
  - Reference the stage name in the COPY instruction
  - Set up your environment:

```
cd docker_images
mkdir multi-stage-builds
cd multi-stage-builds
git clone https://github.com/linuxacademy/content-weather-app.git src
```

- Create the Dockerfile:

```
vi Dockerfile
```

- Dockerfile contents:

```
# Create an image for the weather-app using multi-stage build

FROM node AS build
RUN mkdir -p /var/node/
ADD src/ /var/node/
WORKDIR /var/node
RUN npm install

FROM node:alpine
ARG VERSION=V1.1
LABEL org.label-schema.version=\$VERSION
ENV NODE_ENV="production"
COPY --from=build /var/node /var/node
WORKDIR /var/node
EXPOSE 3000
ENTRYPOINT ["./bin/www"]
```

- Build the image:

```
docker image build -t linuxacademy/weather-app:multi-stage-build --rm --build-arg VERSION=1.5 .
```

- List images to see the size difference:

```
docker image ls
```

- Create the weather-app container:

```
docker container run -d --name multi-stage-build -p 8087:3000 linuxacademy/weather-app:multi-stage-build
```

---

### Tagging

- Add a name and an optional tag with -t or --tag, in the name:tag format:

```
docker image build -t <name>:<tag>
docker image build --tag <name>:<tag>
```

- List your images:

```
docker image ls
```

- Use our Git commit hash as the image tag:

```
git log -1 --pretty=%H
```

- Use the Docker tag to a create a new tagged image:

```
docker tag <SOURCE_IMAGE><:TAG> <TARGET_IMAGE>:<TAG>
```

- Get the commit hash:

```
cd docker_images/weather-app/src
git log -1 --pretty=%H
cd ../
```

- Build the image using the Git hash as the tag:

```
docker image build -t linuxacademy/weather-app:<GIT_HASH> .
```

- Tag the weather-app as the latest using the image tagged with the commit hash:

```
docker image tag linuxacademy/weather-app:<GIT_HASH> linuxacademy/weather-app:latest
```

---

### Distributing Images on Docker Hub

- Create a Docker Hub account:
  `https://hub.docker.com/`

- Docker Push:

```
docker image push <USERNAME>/<IMAGE_NAME>:<TAG>
```

- Creating an image for Docker Hub:

```
docker image tag <IMAGE_NAME>:<TAG> <linuxacademy>/<IMAGE_NAME>:<TAG>
```

- Set up your environment:

```
cd docker_images
mkdir dockerhub
cd dockerhub
```

- Create the Dockerfile:

```
vi Dockerfile
```

- Dockerfile contents:

```
# Create an image for the weather-app using multi-stage build
FROM node AS build
RUN mkdir -p /var/node/
ADD src/ /var/node/
WORKDIR /var/node
RUN npm install

FROM node:alpine
ARG VERSION=V1.1
LABEL org.label-schema.version=$VERSION
ENV NODE_ENV="production"
COPY --from=build /var/node /var/node
WORKDIR /var/node
EXPOSE 3000
ENTRYPOINT ["./bin/www"]
```

- Git the weather-app code:

```
git clone https://github.com/linuxacademy/content-weather-app.git src
```

- Use the Git commit hash as the image tag:

```
cd src
git log -1 --pretty=%H
cd ../
```

- Build the image:

```
docker image build -t <USERNAME>/weather-app:<HASH> --build-arg VERSION=1.5 .
```

- Tag the image before pushing it to Docker Hub:

```
docker image tag linuxacademy/weather-app:<HASH> <USERNAME>/weather-app:<HASH>
```

- Push the image to Docker Hub:

```
docker login
docker image push <USERNAME>/weather-app:<HASH>
```

- Tag the latest image:

```
docker image tag <USERNAME>/weather-app:<HASH> <USERNAME>/weather-app:latest
```

- Push the latest image to Docker Hub:

```
docker login <USERNAME>
docker image push <USERNAME>/weather-app:latest
```

---
