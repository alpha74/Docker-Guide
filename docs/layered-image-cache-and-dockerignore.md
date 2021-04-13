# Layered Image Cache in Docker, and .dockerignore


- `Layered Image Cache` is a way of optimization during docker build by using cached version.
- For large Dockerfiles, this can help reduce `DockerImage` build time.


### Assume a directory structure:
- We will use same dir when [Creating a Docker image for ExpressJS server](https://github.com/alpha74/Docker-Guide/blob/main/docs/create-expressjs-image-cli.md).
- Assume that we have added few more things in our repo, and command `ls -a` in `express` repo gives:
```
.git/    README.md   package.json    node_modules/
Dockerfile      package-lock.json   server.js
```
  - `.git/` : Initialized a git repository here,
  - `README.md` : Created a readme file.
  - `node_modules/` : Ran command `npm install` in this dir.



### Contents of Dockerfile:
- Dockerfile has following data:
```
FROM node
COPY ..
RUN npm install
CMD ["node", "server.js"]
```
- (**Cons**) When we do `docker build` on this image, entire local dir will be copied in the container.
- We notice that, we don't want `.git`, `README.MD` and `node_modules/` in our container.



### Using .dockerignore
- Create a `.dockerignore` file in `express` repo using command: `touch .dockerignore`.
- `.dockerignore` works similarly as `.gitignore` in `git`.
- Write names of all files or folders which we want the Docker to ignore.
- Docker will not copy these files to docker container.
- Contents of `.dockerignore` file:
```
README.md
node_modules/
.git/
```

- This will help not to overload the file system in container.



### Layered Ordering Cache
- For Dockerfile, docker executes the commands in steps.
- As it depletes each step, docker caches over versions of each step.
- Docker only re-runs that step if something in that step has changed. 

- **Eg**: Consider our `Dockerfile`: 
  - Docker will re-run `RUN npm install` when it notices that things in `COPY . .` have changed.

- For our `Dockerfile`, we can optimize the build process by these steps:
  ```
    FROM node
    COPY package.json package.json
    RUN npm install
    COPY server.js server.js
    CMD ["node", "server.js"]
  ```
  - Since, `package.json` is necessary for `npm install` command, we copy it explicity, and immediately run `npm install`.
  - Now, `npm install` won't fire unless we change `package.json`, and will use the cached version.
  - If `package.json` changes, every command after will be run again by docker.
 
 
 
 ### Building DockerImage
- Go to `express` repository in command line.
- Type: `docker build . -t alpha74/express`
- Docker will mention if it is using cached version or not in commandline.
