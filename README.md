# Learning-Docker
Based upon : https://www.udemy.com/course/docker-kubernetes-the-practical-guide/

---

Builds an image from current dockerfile

`docker build .`

---

`docker ps`

Shows the list of running containers

```
CONTAINER ID   IMAGE                       COMMAND                  CREATED          STATUS          PORTS                    NAMES
258a8b3d4356   c0e                         "docker-entrypoint.s…"   17 minutes ago   Up 17 minutes   0.0.0.0:8081->8081/tcp   flamboyant_faraday
```

---

`docker stop 258a8b3d4356`

Stops a running container

---

`docker run node`

Fetch image from docker hub and create container based upon this image

---

`docker ps -a`

List docker processes images and containers

---

`docker run -it node`

Docker run an interactive session from host to container(node)

---

Containers are running instances of images.

---

FROM node : downloads the image from docker hub to local

WORKDIR /app : specifies the work directory where the subsequent commands will be executed

COPY . /app : Copy everything from local dir to /app folder on guest container

RUN npm install : run command while building image

EXPOSE 8081

CMD ["node", "server.js"] : Runs this command only when a container is exectued, not when the image is created.

---

Creating a custom image based upon our code:

```
VSHARMA@MAC ~/Learning-Docker/nodejs-app-starting-setup main % docker build .          
Sending build context to Docker daemon  43.01kB
Step 1/6 : FROM node
 ---> c080a37e3dd2
Step 2/6 : WORKDIR /app
 ---> Using cache
 ---> 1cf07122be05
Step 3/6 : COPY . /app
 ---> 4173d1180b60
Step 4/6 : RUN npm install
 ---> Running in 7d1f6c40a1c0

added 74 packages, and audited 75 packages in 1s

7 packages are looking for funding
  run `npm fund` for details

2 high severity vulnerabilities

To address all issues, run:
  npm audit fix --force

Run `npm audit` for details.
npm notice 
npm notice New minor version of npm available! 9.5.1 -> 9.6.2
npm notice Changelog: <https://github.com/npm/cli/releases/tag/v9.6.2>
npm notice Run `npm install -g npm@9.6.2` to update!
npm notice 
Removing intermediate container 7d1f6c40a1c0
 ---> c21df12a48ff
Step 5/6 : EXPOSE 8081
 ---> Running in ecc1df56c469
Removing intermediate container ecc1df56c469
 ---> eb75d2c0a76f
Step 6/6 : CMD ["node", "server.js"]
 ---> Running in b7a015945edd
Removing intermediate container b7a015945edd
 ---> 28170ca56cd8
Successfully built 28170ca56cd8
```

`28170ca56cd8` this is the image id

---

Run a container based upon image id

`docker run 28170ca56cd8` - starts a node server on the container.

Since the ports were not exposed this node server will not be accessible from Host OS.

---

How to kill this container :

Open new terminal and run

`docker ps` - only shows the running processes

```
% docker ps              
CONTAINER ID   IMAGE                       COMMAND                  CREATED         STATUS         PORTS      NAMES
0f0e9c7b6fd7   28170ca56cd8                "docker-entrypoint.s…"   2 minutes ago   Up 2 minutes   8081/tcp   quirky_pike
```


`docker stop quirky_pike` - will stop the container


Will show the stoped processes too
```
 % docker ps -a           
CONTAINER ID   IMAGE                       COMMAND                  CREATED             STATUS                        PORTS     NAMES
0f0e9c7b6fd7   28170ca56cd8                "docker-entrypoint.s…"   3 minutes ago       Exited (137) 10 seconds ago             quirky_pike
258a8b3d4356   c0e                         "docker-entrypoint.s…"   About an hour ago   Exited (137) 49 minutes ago             flamboyant_faraday
```

---

-p means publish - docker run -p local_port:docker_container_exposed_port image_hash

`docker run -p 3000:80 28170ca56cd8`

---