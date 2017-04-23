# docker-intro
Introduction to Docker, Docker Compose, and Docker Swarm for a class I'm teaching at Jive

## Create Docker image for use in following examples
Build a Docker image with Apache web server hosting the files from the
image/public-html directory. 
```
cd image
docker build -t docker-intro-image .
```
Now run a container called "docker-intro-run" with the image you've just built
```
docker run --name docker-intro-run -d -p 80:80 docker-intro-image
```

## Dockerfile

## Docker-Compose

## Docker Swarm
