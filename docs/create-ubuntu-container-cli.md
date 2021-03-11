# Creating Official Ubuntu Container using CLI


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
- We have not started out container, hence it is not listed.
- Type command: `docker container ls -a` to list all containers.
- Our container will be displayed with state **Created**.
