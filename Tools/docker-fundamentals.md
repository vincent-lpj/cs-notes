## Section 1: Quick Start

#### 1. What is Docker in 2025? Three Innovations

Read this [course](https://github.com/BretFisher/udemy-docker-mastery/blob/main/intro/what-is-docker/what-is-docker.md) in Github

- Build: the container image
  - Dockerfile
  - Image Layers
  - `docker build`
- Ship: the Docker registry
  - Image SHA Hash xxx
  - `Docker.io` , etc.
- Run: the Docker container
  - `docker run`

#### 2. Quick Container Run

[Play with Docker](https://www.docker.com/play-with-docker/)

#### 3. Why Container? Why Now in 2025?

- Isolation
- Environments
- Speed

## Section 2: Course Introduction

#### 4. Course Roadmap (overview)

- Getting Requirements
- Docker Install
- Container Basics
- Image Basics
- Docker Networking
- Docker Volumes
- Docker Compose
- Orchestration
- Docker Swarm
- Kubernetes
- Swarm & K8s

#### 5. Getting Course Resources (GitHub Repo)

[Git Registry For this Course](https://github.com/bretfisher/udemy-docker-mastery)

[Docker Cheat Sheet](https://docs.docker.com/get-started/docker_cheatsheet.pdf)

## Section 3: The Best Way to Setup Docker for Your OS

#### 9. Install The Right Docker for This Course

Lots of ways to run Docker.

- Docker Inc now focused on local Docker Desktop
  - Docker Desktop is like a tool bundler.
    - Engine
    - CLI
    - Compose
    - BuildKit
    - Kubernetes
    - scan, sbom & more
  - Docker Desktop does not run on the server, Docker Engine does.
- Linux containers require a Linux Kernel (OS)
- 3 major ways to run containers
  - Locally (Docker Desktop, RD)
  - Servers (Docker Engine K8S)
  - PaaS (Cloud Run, Margate)

#### 15. VS Code for DevOps, Docker, and YAML Editing

###### Extensions

- Docker
- Kubernetes
- Remote Development
- Live Share

## Setion 4: Creating and Using Containers Like a Boss

#### 17. Check Our Docker Install and Config

###### Section Goals

- Check versions of our docker cli and engine
- Create a Nginx (web server) container
- Learn common container management commands
- Learn Docker networking basics

###### Check Version and Infos

```bash
# List all available Docker commands and subcommands
# Shows the main CLI command groups (run, build, pull, etc.)
docker


# Show Docker client and server version information
# Used to check CLI–Daemon connection and compatibility
docker version


# Display detailed Docker system information
# Includes storage driver, resource limits, OS, and runtime info
docker info
```

###### Docker Command Format

```bash
# New "management commands" format
docker <command> <sub-command> (options)

# old way
docker <command> (options)
```

#### 18. Starting a Nginx Web Server

###### Image vs. Container

An `image` is the application we want to run.

A `container` is an instance of that image running as a process, many containers can be running off the **same** image

###### Nginx Web Server

In this course, the image will be nginx web server

- Download image `nginx` from Docker Hub
  - The default registry is Docker Hub
- Start a new container from that page
- Opened port 80 on the host IP
- Routes that traffic to the container IP, port 80
- Use `ctrl + C` to exit

```bash
# Run an nginx container and map host port 80 to container port 80 (foreground mode)
# Start container in attached/interactive mode
docker container run --publish 80:80 nginx


# Run an nginx container in detached mode (run in background)
# -d / --detach means run in background
docker container run --publish 80:80 --detach nginx


# List all running containers
# Shows container ID, image, status, ports, etc.
docker container ls


# Stop a running container by its container ID
# You only need the first few characters of the ID
docker container stop <container_id>
```

###### run vs. start

`docker container run` always starts a **new** container.

`docker container start` can start an existing stopped one.

```bash
# Run an nginx container in detached mode and name it "webhost"
# Map host port 80 to container port 80
docker container run --publish 80:80 --detach --name webhost nginx


# Show logs for the specified container
# Used for debugging and monitoring
docker container logs webhost


# Display running processes inside the container
# Similar to "ps" on Linux
docker container top webhost


# Stop the running container
docker container stop webhost


# Start a stopped container
docker container start webhost


# Remove the container
# Container must be stopped before removal
docker container rm webhost
```

#### 19. Debrief: What Happens When We Run a Container

###### What Happens in `docker container run`

In the background, Docker will

- look for image locally in image cache, if nothing found
- look in remote image repository, and downlloads the latest for default (nginx:lates by default)
- Create new container based on that image and prepares to start
- Gives it a virtual IP on a private network inside docker engine
- Opens up port 80 on host and forwards to port 80 in container
- Starts container by using the CMD in the image Docker file

```bash
# 8080:80   change host listening port
# 1.11 change version of image
# nginx -T change CMD run on start
docker container run --publish 8080:80 --name webhost -d nginx:1:11 nginx -T
```

#### 20. Container vs. VM: It's Just a Process

Some people compare container with virtual machines, however, containers are not mini virtual machines.

#### 22 & 23. Manage Multiple Containers

###### Assignment

1. Run a `nginx` a `mysql` and a `httpd` (apache) server
2. Run all of them `--detach` (or `-d`), name them with `--name`
3. `nginx` should listen on `80:80`, https on `8080:80`, mysql on `3396:3396`
4. When running `mysql`, use the `--env` option (or `e`) to pass in `MYSQL_RANDOM_ROOT_PASSWORD = true`
5. Use `docker container logs` on mysql to find the random password it created on startup
6. Clean it all upwith `docker container stop` and `docker container rm` (both can acccept multiple names or ID's)
7. Use `docker container ls` to ensure everything is correct before and after cleanup

###### Answers

```bash
docker container run -d -p 3306:3306 --name db -e MYSQL_RANDOM_ROOT_PASSWORD=true mysql
docker container run -d --name webserver -p 8080:80 httpd
docker container run -d --name proxy -p 80:80 nginx

curl localhost
curl localhost:8080

docker container stop httpd nginx db
docker container rm httpd nginx db
```

#### 24. What is Going on in Containers: CLI Process Monitoring

- `docker container top` - process list in one container
- `docker container inspect` - details of one container config
- `docker container stats` - performance stats for **all** containers

####

#### 25. Getting a Shell Inside Containers: No Need for SSH

###### Shell Commands

> When we run `docker container run --help`, we will see:
>
> Usage: docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]

- `docker container run -it` - start new container interactively
- `doceker container exec -it` - run additional command in existing container

###### Examples

```bash
# -t : Allocate a pseudo-TTY (simulate a real terminal, like SSH)
# -i : Keep STDIN open (interactive mode)
# Used together to run an interactive shell
docker container run -it --name proxy nginx bash


# Run an Ubuntu container in interactive mode with a shell
# Default command is /bin/bash (or /bin/sh)
docker container run -it --name ubuntu ubuntu


# Inside the container shell (example prompt)
# root@<container_id>:/# ls -al
# root@<container_id>:/# exit   # Exit the container and stop it
```

#### 27. Docker Networks: Concepts for Private and Public Comms in Containers

###### Docker Network Defaults

All containers on a virtural network can talk to each other

- Each container connected to a private virtual network `bridge`
  - This defaults works well in many cases, but easy to swap out parts to customize it
  - We can make **new** virtual networks
- Containers can be attached to more than one virtual network

###### -p (--publish)

Publishing ports is always in `HOST:CONTAINER` format

```bash
# Run nginx in detached mode and map host port 80 to container port 80
# Host port 80 -> Container port 80
docker container run -d -p 80:80 --name webhost nginx


# Show port mappings of the container
# Display how container ports are exposed on the host
docker container port webhost
# 80/tcp -> 0.0.0.0:80   (All IPv4 addresses)
# 80/tcp -> [::]:80     (All IPv6 addresses)


# Get container internal IP address from bridge network
# Internal IP is only accessible inside Docker host/network
docker container inspect --format '{{ .NetworkSettings.Networks.bridge.IPAddress }}' webhost
# Example output: 172.17.0.2
```

#### 29. Docker Networks: CLI Management of Virtual Networks

###### CLI to be Learnt

- Show networks `docker network ls`
- Inspect a network `docker network inspect <network-name>`
- Create a network `docker network create <network-name>`
- Attach a network to container `docker network connect <network-name> <container-name>`
- Detach a network from container `docker network disconnect <network-name> <container-name>`

###### Tutorial

```bash
# List all Docker networks
# Show default and user-defined networks
docker network ls
# bridge : default NAT network
# host   : use host network directly (no isolation)
# none   : no network access


# Show detailed configuration of the default bridge network
# Includes subnet, gateway, and connected containers
docker network inspect bridge


# Create a user-defined bridge network
# Provides automatic DNS and better isolation
docker network create my_app_net


# Run nginx container and attach it to custom network
# Container will get an IP from my_app_net subnet
docker container run -d --name new_nginx --network my_app_net nginx


# Inspect custom network and list connected containers
# new_nginx should appear in the Containers section
docker network inspect my_app_net
```

###### Default Security

- Create your apps so frontend/backend sit on same Docker network
- Their inter-communication never leaves host
- All externally exposed ports closed by default
- You must mannually expose via `-p`

#### 30. Docker Networks: DNS and How Container Find Each Other

###### Goal

- Understand DNS is the key to easy inter-container comms
  - Docker daemon has a built-in DNS server that containers use by default
  - Static IP's and using IP's for talking to containers is an anti-pattern. Do your best to aviod it
- See how it works by defaults with **costom networks**
  - In a costum network, containers can talk to each other by their name (auto DNS resolution)
  - Docker defaults the hostname to the container's name
- Learn how to use `--link` to enable DNS on default `bridge` network

###### Tutorial

```bash
# Suppose we have two nginx containers in the same custom network
# Both containers are attached to "my_app_net"
docker container run -d --name new_nginx --network my_app_net nginx
docker container run -d --name my_nginx  --network my_app_net nginx


# Inspect the custom network
# Show connected containers and their IP addresses
docker network inspect my_app_net


# Enter one nginx container for debugging
# NOTE: nginx image usually does NOT include bash
# Use "sh" instead if bash is not available
docker container exec -it my_nginx bash


# Update package index inside container
apt update


# Install ping tool (iputils package)
apt install -y iputils-ping


# Test Docker DNS
# Resolve container name "new_nginx" to its internal IP
ping new_nginx
```

#### 31 & 32. Assignments : Using Containers for CLI Testing

###### Assignments

- Use different Linux distro containers to check `curl` CLI Tool version
- Use two different terminal windows to start `bash` in both `centos:7` and `ubuntu:14.04`, using `-it`
- Learn the `docker container --rm` option so you can save clean up
- Ensure `curl` is installed and on latest version for that distro
  - ubuntu: `apt-get update && apt-get install curl`
  - centos: `yum update curl`
- Check `curl --version`

###### Answer

```bash
# Run a CentOS 7 container in interactive mode and remove it after exit
# CentOS 7 comes with curl pre-installed
docker container run -it --rm centos:7


# Check curl version in CentOS container
curl --version
# Example output: curl 7.29.0


# Run an Ubuntu 14.04 container in interactive mode and remove it after exit
# Ubuntu 14.04 does NOT include curl by default
docker run -it --rm ubuntu:14.04


# Update package index and install curl in Ubuntu
apt-get update && apt-get install -y curl
# Check curl version in Ubuntu container
curl --version
# Example output: curl 7.35.0
```

## Section 5: Container Images, Where to Find Them and How to Build Them

#### 36. What's In An Image (and What Is Not)

###### Section Goals

- All about image, the buidling blocks of containers
- What's in an image (and what is not)
- Using Docker Hub Registry
- Managing our local image cache
- Building our own images

###### What is in An Image

Official Definition: An image is an ordered collection of root filesystem changes and the cprresponding execution parameters for use within a container runtime.

- App binaries and dependencies
- Metadata about the image data and how to run the image
- Not a complete OS. No kernel.Small as a file is possible

#### 37. The Might Hub: Using Docker Hub Registry Images

###### Lecture Goal

- Basics of Docker Hub
- Find Official and other good public images
  - Official image does not have a forward slash `/` in the name
  - `Dockerfile` of official images can be seen: [Nginx](https://github.com/nginx/docker-nginx/blob/ffe72978e08c5b0dacecd604e528f6d0741a9ae5/mainline/debian/Dockerfile)
- Download images and basics of image tags
  - `docker pull nginx:1.11.9`

###### Tutorial

```bash
# Pull the latest version of nginx image from Docker Hub
# "latest" usually points to the newest stable release
docker pull nginx:latest


# Pull a specific version of nginx image
# Useful for version control and reproducible environments
docker pull nginx:1.11.9


# List all local Docker images
# Show repository, tag, image ID, size, and creation time
docker image ls
```

#### 38. Images and Their Layers: Discover the Image Cache

###### Lecture Goals

- Image layers
  - Every Docker image starts from a base layer called `scratch`
    - `scratch` represents an empty filesystem
  - Each instruction in a Dockerfile creates a new **read-only layer**
  - Every layer has a unique SHA256 digest
    - Used to identify and reuse layers
    - Enables layer caching
- Union file system
  - Multiple read-only layers are stacked together
- `docker image history` and `docker image inspect` commands
  - history commands allow us to see layer history
- Copy on write
  - Image layers are read-only
  - A container is just a single read/write layer on top of image
  - When a container modifies a file:
    - The file is copied into a new writable layer
    - Only the changed file is stored

###### Tutorial

```bash
# List all local Docker images
# Show repository, tag, image ID, size, and creation time
docker image ls


# Show image build history (image layers)
# Display each layer created by Dockerfile instructions
docker image history nginx:latest


# Return detailed image metadata in JSON format
# Includes layers, environment variables, entrypoint, and config
docker image inspect nginx:latest
```

#### 39. Image Tagging and Pushing to Docker Hub

###### Lecture Goal

- All about image **tags**
  - `docker image tag <source_image:tag> <target_image:tag>`
- How to upload to Docker Hub
- Image ID vs. Tag
  - Tagging does not influence image ID

###### Tutorial

```bash
# Create a new tag for an existing image
# Tag nginx image for pushing to Docker Hub
docker image tag nginx my_username/nginx:testing


# List local images
# Verify that both images share the same IMAGE ID
# nginx and my_username/nginx:testing point to the same image
docker image ls


# Log in to Docker Hub
# Authenticate with username and password/token
docker login


# Push the tagged image to Docker Hub
# Upload image layers to remote registry
docker image push my_username/nginx:testing


# Log out from Docker Hub
# Remove stored authentication credentials
docker logout
```

#### 40. Building Images: The Dockerfile Basics

[Writing a Dockerfile](https://docs.docker.com/get-started/docker-concepts/building-images/writing-a-dockerfile/)

```dockerfile
FROM python:3.13
WORKDIR /usr/local/app

# Install the application dependencies
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

# Copy in the source code
COPY src ./src
EXPOSE 8080

# Setup an app user so the container doesn't run as the root user
RUN useradd app
USER app

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8080"]
```

- `FROM <image>` - this specifies the base image that the build will extend.
- `WORKDIR <path>` - this instruction specifies the "working directory" or the path in the image where files will be copied and commands will be executed.
- `COPY <host-path> <image-path>` - this instruction tells the builder to copy files from the host and put them into the container image.
- `RUN <command>` - this instruction tells the builder to run the specified command.
- `ENV <name> <value>` - this instruction sets an environment variable that a running container will use.
- `EXPOSE <port-number>` - this instruction sets configuration on the image that indicates a port the image would like to expose.
- `USER <user-or-uid>` - this instruction sets the default user for all subsequent instructions.
- `CMD ["<command>", "<arg1>"]` - this instruction sets the default command a container using this image will run.

#### 41. Building Images: Running Docker Builds

###### Sample Dockerfile: custom nginx

```bash
# Build a Docker image from Dockerfile in current directory
# Tag the image as "customnginx"
docker image build -t customnginx .


# List local images
# Verify that the new image has been created
docker image ls


# Rebuild the same image
# Docker will reuse cached layers if Dockerfile has not changed
docker image build -t customnginx .


# Note:
# Docker uses layer caching to speed up builds
# Unchanged layers are reused from cache
# Changed layers are rebuilt
#
# Best practice:
# Put rarely changed instructions at the top
# Put frequently changed instructions at the bottom
# This improves build performance
```

#### 42. Building Images: Extending Official Images

###### Sample Dockerfile: nginx-with-html

`Dockerfile`

```dockerfile
# this shows how we can extend/change an existing official image from Docker Hub

FROM nginx:latest
# highly recommend you always pin versions for anything beyond dev/learn

WORKDIR /usr/share/nginx/html
# change working directory to root of nginx webhost
# using WORKDIR is preferred to using 'RUN cd /some/path'

COPY index.html index.html

# I don't have to specify EXPOSE or CMD because they're in my FROM
```

`index.html`

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8" />

    <title>Your 2nd Dockerfile worked!</title>
  </head>

  <body>
    <h1>
      You just successfully ran a container with a custom file copied into the
      image at build time!
    </h1>
  </body>
</html>
```

`bash command`

```bash
# Run official nginx container and map host port 80 to container port 80
# Remove container automatically after exit
docker container run -p 80:80 --rm nginx


# Access the service from host browser
# Open http://localhost in a web browser
# You should see the default "Welcome to nginx" page


# Build a custom nginx image with custom HTML content
# Dockerfile should copy local HTML files into nginx web root
docker build -t nginx-with-html .


# Run the custom nginx image and expose port 80
# Serve custom HTML page instead of default page
docker run --rm -p 80:80 nginx-with-html
```

#### 43 & 44. Assignment: Build Your Own Dockerfile and Run Containers From It

###### Assignment

Take existing Node.js app and Dockerize it.

- Make `Dockerfile` and build it.
- Run it
- Use the `Alpine` version of the official `node` 6.x image
- Expect result is web site at `http://localhost`
- Tag and Push it

Details of the assignment:

- you should use the `node` official image, with the alpine 6.x branch (`node:6-alpine`)
  - (Yes this is a 2-year old image of node, but all official images are always available on Docker Hub forever, to ensure even old apps still work. It is common to still need to deploy old app versions, even years later.)
- This app listens on port 3000, but the container should listen on port 80 of the Docker host, so it will respond to [http://localhost:80](http://localhost/) on your computer
- Then it should use the alpine package manager to install tini: `apk add --no-cache tini`.
- Then it should create directory /usr/src/app for app files with `mkdir -p /usr/src/app`, or with the Dockerfile command `WORKDIR /usr/src/app`.
- Node.js uses a "package manager", so it needs to copy in package.json file.
- Then it needs to run 'npm install' to install dependencies from that file.
- To keep it clean and small, run `npm cache clean --force` after the above, in the same RUN command.
- Then it needs to copy in all files from current directory into the image.
- Then it needs to start the container with the command `/sbin/tini -- node ./bin/www`. Be sure to use JSON array syntax for CMD. (`CMD [ "something", "something" ]`)
- In the end you should be using FROM, RUN, WORKDIR, COPY, EXPOSE, and CMD commands

###### Answer

`Dockefile`

```
FROM node:6-alpine

EXPOSE 3000

RUN apk add --no-cache tini

WORKDIR /usr/src/app

COPY package.json ./package.json

RUN npm install && npm cache clean --force

COPY . .

CMD ["/sbin/tini", "--", "node", "./bin/www"]
```

`bash`

```
docker container build -t testnode .
docker container run --rm -p 80:3000 testnode
```

## Section 6 Presistent Data: Volumes

#### 46. Container Lifetime & Persistent Data

###### Section Overview

- Defining the problem of **persistent** data
- Key concepts with containers: **immutable**, **ephemeral**
- Learning and using **Data Volumes**
- Learning and using **Bind Mounts**

###### Container Lifetime & Persistent Data

- **immutable infrastructure**: only re-deploy containers, never change
  - What about databases, or unique data?
  - This is known as **persistent data**
- Docker has two ways to deal with this problem
  - `Volumes`: make special location outside of container UFS
  - `Bind Mounts`: link container path to host path

#### 47. Persistent Data: Data Volumes

In the [Dockerfile Reference](https://docs.docker.com/reference/dockerfile/), `VOLUME` keyword is used to create volume mounts.

For example, in the Dockerfile of `mysql`, we will see:

```dockerfile
VOLUME /var/lib/mysql
```

This means everything that we put into the container will outlive the container and saved in this path.

Note that in Windows or MacOS, a Linux VM is created, so we can not see volume directly

```bash
# Run MySQL container without a password (for testing only)
# WARNING: Not safe for production
docker container run -d --name mysql \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=True \
  mysql


# Run MySQL container with a named volume for data persistence
# Store MySQL data in volume "mysql-db"
# NOTE: Correct path is /var/lib/mysql
docker container run -d --name mysql \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=True \
  -v mysql-db:/var/lib/mysql \
  mysql


# Show logs of the MySQL container
# Used to check startup status and errors
docker container logs mysql


# Inspect container configuration and mounts
# Show volume bindings and metadata
docker container inspect mysql

# Example output (Volumes section):
# "Volumes": {
#   "/var/lib/mysql": {}
# }

# Volume information can also be found in "Mounts" section


# List all Docker volumes
# Volumes persist even after containers are deleted
docker volume ls
# DRIVER    VOLUME NAME
# local     mysql-db


# Inspect detailed volume information
# Show mount point and usage
docker volume inspect mysql-db
```

#### 49. Persistent Data: Bind Mounting

`Bind Mounting` basically maps a host file or directory to a container file or directory.

> -v <source>:<target>[:options]

```bash
# Change directory to the project folder
# This directory contains Dockerfile and index.html
cd /**/dockerfile-sample-2


# List files in current directory
# Should show Dockerfile and index.html
ls
# Dockerfile  index.html


# Run nginx container with bind mount
# Mount current host directory to nginx web root
# $(pwd) gets the current absolute path
# Host files will be served directly by nginx
docker container run -d \
  --name nginx-mount \
  -p 80:80 \
  -v $(pwd):/usr/share/nginx/html \
  nginx



# Enter the running nginx container
# Used for debugging and verification
docker container exec -it nginx-mount bash


# Change directory to nginx web root inside container
# This path is mounted from the host directory
cd /usr/share/nginx/html


# List files inside the container
# Should match the host directory contents
ls
# Dockerfile  index.html
```

#### 52 & 53. Assignment: Database Upgrades with Named Volumes

###### Assignment

- Create a `postgres` container with named volume `psql-data` using version `15.1`
- Use Docker Hub to learn `VOLUME` path and versions needed to run it
- Check logs, stop container
- Create a new `postgres` container with **same** named volume using` 15.2`
- Check logs to validate

###### Answer

In Docker Hub, we can see [postgres:15.1](https://hub.docker.com/layers/library/postgres/15.1/images/sha256-978fc12e3db4faf626b01d64b206e262feca9b61f1be74b6f184430987c5505c) has the following settings:

> VOLUME [/var/lib/postgresql/data]

```bash
# Run PostgreSQL 15.1 container with a named volume
# Data will be stored in volume "psql-data"
docker container run -d \
  --name postgres-before \
  -e POSTGRES_PASSWORD=password \
  -v psql-data:/var/lib/postgresql/data \
  postgres:15.1


# Check PostgreSQL startup logs
# Should show database initialization on first run
docker container logs postgres-before


# Stop the container (data remains in volume)
docker container stop postgres-before


# Run a new PostgreSQL container with a newer patch version (15.2)
# Reuse the same named volume "psql-data"
docker container run -d \
  --name postgres-after \
  -e POSTGRES_PASSWORD=password \
  -v psql-data:/var/lib/postgresql/data \
  postgres:15.2


# Check logs again
# Should NOT reinitialize database
# Should reuse existing data directory
docker container logs postgres-after


# Stop the upgraded container
docker container stop postgres-after


# List all volumes
# Verify that "psql-data" still exists
docker volume ls
```

#### 56 & 57. Assignment: Edit Coding Running In Containers With Bind Mounts

###### Assignment

[Jekyll: transform your plain text into static websites and blogs](https://jekyllrb.com/)

Use a Jekyll `Static Site Generator` to start a local web server

- Source code is in the course repo under [bindmount-sample-1](https://github.com/BretFisher/udemy-docker-mastery/tree/main/bindmount-sample-1)
- We edit files with editor on our host using native tools
- Container detects changes with host files and updates web server
- Start container with `docker run -p 80:4000 -v $(pwd):/site bretfisher/jekyll-serve`

###### Answer

```bash
# Change directory to the Jekyll project folder
# This directory contains site source files (_posts, _config.yml, etc.)
cd /**/bindmount-sample-1


# List files in current directory
# Should show Jekyll project structure
ls


# Run Jekyll server in a Docker container with bind mount
# Map host port 80 to container port 4000 (Jekyll default port)
# Mount current directory to /site inside the container
# Jekyll will read site files from /site
docker container run \
  -p 80:4000 \
  -v $(pwd):/site \
  brefisher/jekyll-serve


# After editing markdown files in the _posts folder
# Jekyll will automatically rebuild the site
# Changes will be reflected in the browser
# Access via: http://localhost
```

## Section 7: Dockerfile ENTRYPOINT

#### 58. Intro: Review before ENTRYPOINT

In this section, we will focus on `ENTRYPOINT` section.

```dockerfile
FROM python:slim

ENV PYTHONUNBUFFERED=1

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . .

EXPOSE 8000

CMD ["python", "main.py"]
```

#### 59. Buildtime vs. Runtime

Two questions you should consider when write any statements in your Dockerfile:

- Does it overwrite its previous use?
  - Overwrite (`WORKDIR`, `CMD`) vs. Additive (`EXPOSE`, `ENV`)
- Does it change my image or the container
  - Buildtime (`FROM`, `COPY`, `RUN`) vs. Runtime (`EXPOSE`, `VOLUME`, `ENTRYPOINT`, `CMD`)

#### 60. What's An ENTRYPOINT

`ENTRYPOINT` is the default executable when a container starts.

It acts differently from `CMD`

- Use `CMD` as default
- `ENTRYPOINT` can accomplish `CMD` when using together

```bash
# Inspect busybox image metadata
# Check default command (CMD) defined in the image
docker image inspect busybox

# Example output:
# "Cmd": [
#   "sh"
# ]
# This means the container will run "sh" by default when started


# Run busybox in interactive mode
# -i keeps STDIN open
# -t allocates a pseudo-TTY
# Needed because default command is "sh" (interactive shell)
docker container run --rm -it busybox


# Override the default command
# Instead of running "sh", run "date"
# This replaces the image's default CMD
docker container run --rm busybox date
```

#### 61. Using ENTRYPOINT and CMD Together

When **both** `ENTRYPOINT` and `CMD` is set:

- Docker will combine them into a **single string** with a space between them and execute
- It can be used in the following cases:
  - CLI tools
    - Use `ENTRYPOINT` to set the base executable, while `CMD` provides default arguments
  - Startup Scripts
    - Use `ENTRYPOINT` to set the script, and `CMD` to set the final process

Suppose we have an image built from a Dockerfile like below:

```dockerfile
FROM ubuntu:latest

RUN apt-get update &&\
		apt-get install -y --no-install-recommends \
		curl \
		&& rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["curl"]

CMD ["--help"]
```
