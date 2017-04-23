# docker-intro
Introduction to Docker, Docker Compose, and Docker Swarm for a class I'm teaching at Jive

## Create Docker image for use in following examples
Build a Docker image with Apache web server hosting the files from the
public-html directory. 
```
docker build -t docker-intro-image .
```
Note that the Docker Hub will automatically build this Docker image thanks to the built in integration between Docker Hub and Github

## Dockerfile with Docker run
Now run a container called "docker-intro-run" with the image you've just built
```
docker run --name docker-intro-run -d -p 80:80 docker-intro-image
```

Open up a web browser to "http://localhost" (or the IP/hostname of the Docker host on port 80) and you should now see the sample 
webpage with a meme.

When you're ready for the next method, make sure to stop (and optionally clean up) your Docker container. Be sure to leave 
the Docker image "docker-intro-image" behind as you'll use it in the other methods. 
```
docker stop docker-intro-run
# optionally
docker kill docker-intro-run
```

## Docker-Compose
Docker Compose uses specially formatted docker-compose.yaml files to store configuration information for a Docker Compose build.
In this first example, our docker-compose.yaml is running the exact same image as our Dockerfile example, but is exposing
web traffic on port 8080 and passing that through to a load balancer (provided by the ha proxy container) instead of just 
exposing directly on port 80. 

To run the Docker Compose version of our image, do the following:
```
docker-compose -f docker-compose.yaml up -d
```

The purpose of setting up our Docker Compose example with a load balancer is so we can scale up our web application (in our example,
the Apache container serving public-html files). To do this, use the scale functionality of Docker Compose:
```
docker-compose scale web=5
```

Again, check that our web page is up at http://localhost. Also, ensure that your requests to the web page are being properly load balanced
across the five containers by watching the logs and refreshing the web page:
```
docker-compose logs -f
```

When you're done, shut down your compose build. Note this will remove the "front-tier" network bridge which Docker Compose created as well. 
```
docker-compose down
```

## Docker Swarm
