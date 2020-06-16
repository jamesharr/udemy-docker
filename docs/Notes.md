https://udemy.com/course/docker-and-kubernetes-the-complete-guide

# Quick Commands
* Creating and Starting
  * `docker create hello-world`
  * `docker start -a ID` Start and attach using `-a` 
  * `docker run hello-world` - Create and Start
  * `docker run -it redis`
  * `docker run busybox`
  * `docker run busybox ls`
  * `docker run xyz -p 8080:8080` - redirect port (first to second)
  * `docker exec -it ID CMD` - Execute an additional command inside a container.
  * `docker exec -it ID sh` - Shell, use ctrl-d to exit
* Managing containers
  * `docker ps`
  * `docker ps --all`
  * `docker logs ID`
  * `docker rm ID`
  * `docker stop ID` - SIGTERM, SIGKILL after 10sec (use `--time=30` to tweak)
  * `docker kill ID` - SIGKILL immediately
* Misc docker management
  * `docker system prune` - delete all unused containers, images, etc
  * `docker images`

# Dockerfile
```dockerfile
# Dockerfile
FROM alpine
RUN apk install --update xyz
WORKDIR /usr/app              # Automatically created if it does not exist, affects CMD as well
COPY ./src ./dst
CMD ["foo-server"]
```
* `docker build .`
* `docker build -t jamesharr/image-name:latest [CONTEXT] .`
* `docker build -t jamesharr/image-name [CONTEXT] .` - latest is assumed and automatically appended
* `docker commit -c "CMD ['my-command']" ID` - manually create a snapshot of a container

```dockerfile
# Dockerfile.dev

```

# Docker Compose
```yaml
# docker-compose.yml
version: '3'
services:
    redis-server:
        image: 'redis'
    node-app:
        build: .
        ports:
            - "4001:8081"
```

* `docker-compose up`
* `docker-compose up --build`
