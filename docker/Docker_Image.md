# Docker Image

## How to start

Create a File called `Dockerfile` without any extension with following example structure:

````docker
# Use an existing docker image as a base
From alpine
# Download and install a dependency
RUN apk add --update redis
#Tell the image what to do when it starts as a container
CMD ["redis-server"]
 ````

Then build the image via the command line through running within the directory of the Dockerfile follwing command:

 `docker build .`

 After that run the container while calling `docker run <containerID>`

 ## Convention for Tagging

 For giving a tag to a docker file there is a strict convention which should be used. The convention looks like

 `docker build -t <YourDockerID>/<repo/Project name>:<version>`

 The version is always called `latest` for the latest image

 Example :

 `docker build -t kn0rr/redis-server:latest .`

 Then you can run the image by `docker run kn0rr/redis-server` , by default the "latest" image is used

 ## Create an own image out of an running container

If you want to create an image out of an running container with some additional commands you can do it like following.

````docker
# run the container and start an interactive shell
docker run -it alpine sh
# do some stuff here which should be done in your new image e.g. install redis
apk add --update redis

`````
Then open a new terminal to do a `docker ps` . 
After that run addtional commands you want to execute within the container while refering to the containerID at the end e.g.  

`docker commit -c 'CMD ["redis-server"]' 776abe4ec8c5`

>NOTE: Within a Windows Terminal the command is a little bit different:
>
> `docker commit -c "CMD 'redis-server'"  776abe4ec8c5`

Then you will get the new Image ID

## Enhanced Build commands

To create in image where you want to integrate some data you need to ehance the `Dockerfile` with some further commands
````docker
# Use an existing docker image as a base
From node:alpine

# Working Directory.Specify to make sure not to copy data into root directory
WORKDIR /usr/app

# Copy the files from the build context into the current working directory 
# of the container. Necessary so that package.json and index. json are 
# available
COPY ./package.json ./

# Download and install a dependency
RUN npm install

# Here you can specify the files you want to copy later, because they 
# change frequently, so that you make the most out of the caching

COPY ./ ./

#Tell the image what to do when it starts as a container
CMD ["npm","start"]


````
