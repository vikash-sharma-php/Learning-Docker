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


