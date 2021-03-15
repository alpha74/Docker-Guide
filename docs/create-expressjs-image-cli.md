# Create ExpressJS Docker Image using CLI

- We will create a Docker image for ExpressJs server.
- We will then create a Docker container from that docker image.


### 1. Create a directory structure:
- Create a directory `express` in `docker` dir.
- Type: `mkdir express`.
- Type: `cd express`.


### 2. Create essential files:
- In dir `express`:
  - Type: `touch Dockerfile`
  - Type: `touch package.json`
  - Type: `touch server.js`


### 3. Edit server.js :
- Add following code in `server.js`. This step requires to have some knowledge of ExpressJs.
```
const express = require('express');
const app = express();
const HOST = "0.0.0.0";
const PORT = 80;

app.get('/', (req, res) => {
  res.send("Index page");  
});

app.listen(PORT, HOST);
console.log(`Running on http://${HOST}:${PORT}`);
```


### 4. Edit package.json :
- Add following code in `package.json`. This step requires to have some knowledge of NodeJs.
```
{
  "dependencies" : {
    "express" : "^4.16.1"
  }
}
```


### 5. Edit Dockerfile
- Add following code in `Dockerfile`:
```
FROM node
COPY . .
RUN npm install
CMD ["node", "server.js"]
```

- `FROM node` : If no tag is used(eg: `node:latest`), latest version is used by default.
- `COPY . .` : Copies complete local directory to container file system.
- `npm install` : Installs packages from `package.json`.
- `CMD ["node", "server.js"]` : Preferred format for execution of commands. Here, no `shell` is invoked.


### 6. Build a Docker Image:
- Go to `express` repository in command line.
- Type: `docker build . -t alpha74/express`.
- `.` indicates that we are building from local path.
- `-t` is used to set name and a tag.
- `alpha74/express` is the image name. Format: `<username>/<image-name>`.
- It will download `node` image from DockerHub and will create a DockerImage, or use a local cache version.


### 7. Viewing our Docker Image:
- Type: `docker image ls`.
- Our docker image will be displayed in the list. Here, it is: `alpha74/express`.


### 8. Run a Docker container using our DockerImage:
- Type: `docker run --name=express -p=3002:80 alpha74/express`.
- This will be printed: `Running on http://0.0.0.0:80`.
- Here, `--name=fileviewer` is used to set a name to container.
- `-p` to route port `3001` of our machine to port `5000` of the container.
- Using this command, our terminal remains **busy**.



### 9. Accessing our ExpressJs server:
- Open browser of your choice, and goto `localhost:3002`.
- `Index page` will be displayed in browser.


-----

### Run Docker container using detach flag:
- Stop the container if already running using: `docker rm -f express`.
- Type: `docker run --name=express -d -p=3002:80 alpha74/express`.
- Docker container will be started without blocking our command line.
- `-d` stands for detach.
