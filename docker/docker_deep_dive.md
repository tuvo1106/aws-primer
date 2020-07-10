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
