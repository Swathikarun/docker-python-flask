# docker-python-flask

This is to create a python-flask web application in docker.

## Requirements

- [Install Docker](https://docs.docker.com/engine/install/)
- [Install Docker Compose](https://docs.docker.com/compose/install/)

## Prerequisite

- Python script - app.py
- Dependency file - requirements.txt

## Building a Docker Image

1. Generate a Dockerfile inorder to build a docker image. Always keep in mind that this file should be placed inside a specific folder. 

```
$ mkdir appdir

$ cd appdir


$ vim Dockerfile

FROM alpine:3.8                       ------->       ### To create temporary container from the base image ###

RUN mkdir /var/flaskapp               ------->       ### Executes the command to create a directory ###

WORKDIR   /var/flaskapp               ------->       ### Reset the default working directory to /var/flaskapp ###

COPY . .                              ------->       ### Copy the contents from local directory to the default working directory of container ###

RUN apk update && apk add python3     ------->       ### Install python3 ###

RUN pip3 install -r requirements.txt  ------->       ### Install all the modules mentioned in dependency file ###

EXPOSE 5000                           ------->       ### Port publishing ###

CMD ["/usr/bin/python3" , "app.py"]   ------->       ### Default command to be executed when container is created ###
```

2. Create a docker image

```
 $ docker build -t swathikarun/devflaskapp:1 .
```

3. Tag the image

```
 $ docker tag swathikarun/devflaskapp:1 swathikarun/devflaskapp:latest
```

4. Push the image to dockerhub

```
 $ docker image push swathikarun/devflaskapp:latest
 $ docker image push swathikarun/devflaskapp:1
```
 
## Download the created image from the repository

```
 $ docker image pull swathikarun/devflaskapp:latest
```
 
## Create a container using this image

```
 $ docker container run --name app -d -p 80:5000 swathikarun/devflaskapp:latest
```

## Docker container logs

 You can check the logs of the docker container using the below command
 
 ```
  $ docker logs app
 ```
 
 ## Result
 
 A web application is created with python-flask in docker.
