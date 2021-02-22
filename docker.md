# Docker Notes

## Running a Docker Image Locally
1. Build a local image
	- cd into the root directory of the project
	- _docker build -t <your name>/<name of image>:latest ._
2. Create a container for the image
	- `$ docker container create -p 9000:8080 --name container_name image_name`
	- OR `$ docker run --name container_name image_name`
3. Run the container and specify ports to expose/publish
	- `$ docker container start -i container_name`
	- OR skip #2 `$ docker run -p 9000:8080 --name container_name image_name`

## Building and Pushing Docker Images
- Login
	- _docker login -p $(oc whoami -t) -u <username> <registry hostname>_
- Build for Remote
	- _docker build -t <registry hostname>/<openshift project name>/<name of image>:latest ._
- Push to Remote
	- _docker push <registry hostname>/<openshift project name>/<name of image>:latest_

## Other Useful Commands
- `$ docker info` - spit out a bunch of info to console
- `$ docker ps -a` - lists all containers
- `$ docker container ls` - list containers (doesn't seem to include all of them)
- `$ docker image ls` - list images
- `$ docker image rm <image1_name> <image2_name>` - remove image(s)
- `$ docker container rm <container1_name> <container2_name>` - remove container(s)
- `$ docker stop <container_name>` - stop a running container
- `$ docker exec -i <container_name> /bin/bash` - open a bash terminal within the container

## Resources
- [Great intro video](https://www.youtube.com/watch?v=YFl2mCHdv24)
- [Good Article](https://codefresh.io/docker-tutorial/java_docker_pipeline/)
- [RE: JVM+Docker -> Memory](https://medium.com/@yortuc/jvm-memory-allocation-in-docker-container-a26bbce3a3f2)
- [OpenJDK Docker Hub](https://hub.docker.com/_/openjdk)

