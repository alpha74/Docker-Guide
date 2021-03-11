# Creating Official Ubuntu Container using CLI



<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3a/Logo-ubuntu_no%28r%29-black_orange-hex.svg/1920px-Logo-ubuntu_no%28r%29-black_orange-hex.svg.png" alt="drawing" width="200" height="50"/>




### 1. Get ubuntu docker image
- Type command: `docker search ubuntu`
- We get a list of all related ubuntu images along with description.
- OFFICIAL keyword tells if the images are official images of docker.
- AUTO keyword tells the images which are automatically detected by Dockerhub.


### 2. Creating ubuntu container
- We will use `docker create` command. Use `docker create --help` to know more about it.
- Type command: `docker --name=foo -it create ubuntu bash`.
- Here:
  - `bash` is the default command line of ubuntu.
  - `--name` is used to set a name to our container.
  - `-i` flag allows the container to be interactable.
  - `-t` flag allows the container to be a text-input and text-output environment. It stand for `tty` or tele-typewriter.

- Docker now downloads ubuntu image to local machine.
- A **hash string** is printed after the command executes, which the generated ID of this container.
- This hash string can be used to interact with container if we don't set a name of container.


### 3. Listing our container
- Type command: `docker container ls`.
- A list of container will appear which are in **Running** state.
- Since we have not started out container, hence it is not listed.
- Type command: `docker container ls -a` to list all containers.
- Our container will be displayed with state **Created**.


### 4. Starting a docker container:
- Type command: `docker start foo` to start the container.



### 5. Getting into Container's file system

- Type command: `docker attach foo`. This changes the state to **Running**.
- Prompt changes to `root` of container with few characters of container's hash string.
- Use `ls` to view file directories.
- Use `Ctrl+P+Q` to escape out of container's directory.
- Note that `Ctrl+D` will stop the container.


### 6. Viewing logs without Attaching to container
- Type command: `docker logs foo`.
- It returns everything typed on container's terminal.
- It can also be used to view what the container is printing out.


------

## More Commands


### Stopping a container:
- Type command: `docker stop foo` or `docker stop <hash>`.
- It might take some time to stop a running container.
- Name of the container is printed after it has stopped.


### Removing a container:
- Note that a running container cannot be removed. We need to stop it first.
- Type command: `docker rm foo` or `docker rm <hash>`.
- Name of container is printed after task completes.
- It removes space used by container.


### Running a container quickly using 'run'
- Both creates and attaches with container.
- Type command: `docker run --name=bar -it ubuntu bash`.
- It immediately attaches to container.


### Force Remove container:
- It stops and removes the container.
- Command: `docker rm -f bar`.


### List all Docker Images:
- Use command: `docker image ls` to list all docker images.



