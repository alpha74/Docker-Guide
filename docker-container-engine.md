# Docker Containers and Docker Engine



### Docker Container:
- It is a loosely isolated environment running within a host machine's kernel that allows us to run applications specific-code.
- Each container gets its own file system independent of other containers.

### Kernel:
- Kernel is the software at the core of operating system with complete control.
- Docker runs on top of machine's kernel, making it a host machine.


### Docker Engine:
- It consists of **Docker Server, an API, and a CLI** to interact with Docker API.
- The Docker server is also called **Docker daemon**.


![Docker Engine](https://github.com/alpha74/Docker-Manual/blob/main/img/docker-engine.png)


### Docker Container Environments:
- Docker engine creates containers on top of kernel.
- Environments provides a degree of isolation.
- The processes of one container cannot affect the processes of another container.
- A container has limits on resource, eg: CPU and memory.


### Need for Docker Containers:
- Allow portability to multiple operating systems, eg: Linux, macOS, cloud platform.
- Less time is needed for setting up the environment. Hence, more focus on application code.
- Isolation allows easy CI/CD and development.

- Better than Virtual machines as a container is more light-weight.
- The file system is strictly separate for VMs, but can be shared by Docker Containers depending on situation.f
