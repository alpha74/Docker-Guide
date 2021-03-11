# Docker Images and Dockerfile



### Docker Images
- They are 'ready-only templates' with instructions for creating a Docker container.
- It defines the container code, libraries, env variables, config files and more.
- To create a docker container from image: `docker create


### Dockerfile:
- It outlines intructions for how a DockerImage will create a container.
- It is a text document with various commands that assemble to build a container.


### Image to Container relationship:
- DockerImage is an assembled set of instructions of how to create a container.
- Many containers can be created from a single assembled image.
- Container is a result of running an image.
- [Dockerhub](https://hub.docker.com/) collects images from Docker users and host them online.
