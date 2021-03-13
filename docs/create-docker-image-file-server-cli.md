# Create a Docker Image for a File Server using CLI

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d9/Node.js_logo.svg/440px-Node.js_logo.svg.png" width=170 height=100>

- We will create a dockerfile and then a docker container for a static file server for a folder inside the container.
- It will called **FileViewer** and uses [**serve**](https://www.npmjs.com/package/serve) package of [Nodejs](https://nodejs.org/en/).
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


### 4. Build a DockerImage from DockerFile
- Inside `fileviewer` directory, type: `docker build . -t alpha74/fileviewer`
- `.` indicates that we are building from local path.
- `-t` is used to set name and a tag.
- It will download `node` image from DockerHub and will create a DockerImage.


### 5. Viewing our DockerImage:
- Type: `docker image ls`
- Our docker image will be displayed in the list. Here, it is: `alpha74/fileviewer`.


### 6. Run a Container using our Docker Image
- Type: `docker run --name=fileviewer -p=3001:5000 alpha74/fileviewer`.
- Here, `--name=fileviewer` is used to set a name to container.
- `serve` module exposes on port `5000` by default, but it is inside the container.
- Container creates its own localhost. Hence, we need `-p` to route port `3001` of our machine to port `5000` of the container.


### 7. Accessing our Web application:
- Open browser of your choice, and goto `localhost:3001`.
- We can now view contents of `display` directory in the browser.
