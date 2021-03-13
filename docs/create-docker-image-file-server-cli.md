# Create a Docker Image for a File Server using CLI


- We will create a static file server for a folder inside a docker container.
- It will called **FileViewer** and uses **serve** package of Nodejs.
- It will be a browser based web application for viewing contents inside a directory.
- Using `bash` command line.


### 1. Create a directory structure
- Create a directory named `fileviewer`(This is an optional step. Skip if you know the usage of `serve` package in nodejs).
- Type: `mkdir fileserver`
- Type: `cd fileserver`

- Create a directory for storing contents which will be shown.
- `mkdir display`.
- Create or add files to displayed.
- Type: `cd display`.
- Type: `touch somefile.txt`

### 2. Create a Dockerfile
- In directory `fileviewer`, type: `touch Dockerfile`.
- The file structure of `fileviewer` should look like this:
```
Dockerfile  display/
```

### 3. Edit the Dockerfile
- Copy these contents in `Dockerfile` created in above step.
```
FROM node:latest
RUN npm install -g serve
COPY ./display ./display
CMD serve ./display
```

- `FROM node:latest`:
  - `FROM` is used to choose a DockerImage.
  - Command to get the latest version of nodejs.
  - You can use `docker search node` to choose an appropriate nodejs image.
  - `latest` keyword fetches the latest image of `node`.

- `RUN npm install -g serve`:
  - `RUN` is used to run an application within a Docker container.
  - This command will install `serve` node package inside the container.
  - `-g` flag makes `serve` to install globally so that it can be accessed anywhere in the container.

- `COPY ./display ./display`:
  - `COPY` copies a local file to container directory. It creates the file if it already not exists.
  - Here, it copies local `display` dir to container file system.


- `CMD serve ./display`:
  - `CMD` is used to use a commandline tool. For Ubuntu: it is `bash`.
  - This command will evaluated by `bash` as `server ./display`



