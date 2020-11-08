# Docker Compose

## Docker Compose File
Good alternative to start multiple containers in a robust manner.
It helps by also giving some more networking options, so you don't need to use the more complex Docker CLI's Networking Features.

The docker-compose file has a basic structure like the one below and its written in YAML format:

````yaml
version: '3'
# in case of Docker a service is most likely a container
services: 
    redis-server:
        # Specify image instead of own build dokerfile
        image: 'redis'
    node-app:
        # Specify dockerfile in the directory
        build: .
        # Specify ports <localPort>:<ContainerPort>
        ports:
            - "4001:8081"
````
![Docker-Compose](img/Docker-compose.svg)

Every Container specified in this YAML file will be created in the **same network**, so the containers have access to each other and you don't need to specify any ports to open for each other!

So if you want to acces tham you can write something like this in the index.js file:
````javascript
// In a traditionall environment you would specify a host like 'https://my-redis-server.com' 
// but since we are using docker-compose we can simply specify the name
// port definition is optional
const client =redis.createClient({
    host:'redis-server',
    port: 6379
});
````


> **REMARK:** The **Port** definition in the **docker-compose file** is only to open Ports to the **local machine!**

## Docker Compose Commands

- **docker-compose up**: The same as `docker run <myimage>`. Instead of defining an image name, docker compose is looking for a docker-compose file in the directory.

- **docker-compose up --build**: This command is equal to `docker build .` and `docker run <myImage>`. So instead of running two separate commands you can use this simple command to re-build all the containers in the yaml-file.

- **docker-compose up -d**: Run all the containers in the background (dettach mode)

- **docker-compose down**: Stop all running containers created by the docker-compose file

- **docker-compose ps**: Shows the Status of the container in the docker-compose file

> Always run the Docker Compose commands within the directory where the docker-compose file exists, because docker-compose is specifically looking for that file!

## Restart policies

There are four restart policies:

- **"no"**: Never attempt ot restart this container if it stops or crashes **(default Policy)**. 
>**No** needs to be specified with single or double quotes because otherwise yaml interprets no as false!

- **always**: If this container stops for any reason always attempt to restart it

- **on-failure**: Only restart if the container stops with an error code

- **unless-stopped** Always restart unless someone forcibly stops it

**Example:**
````yaml
version: '3'
services: 
    redis-server:
        # Specify image instead of own build dockerfile
        image: 'redis'
        restart: "no"
    node-app:
        # Restart policy:
        restart: always
        # Specify dockerfile in the directory
        build: .
        # Specify ports <localPort>:<ContainerPort>
        ports:
            - "4001:8081"
````