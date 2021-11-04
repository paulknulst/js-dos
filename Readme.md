# js-dos example

This project includes a Dockerfile to create a website on which you can play pac-man (shareware).

Live-Demo: https://js-dos.f1nalboss.de/pac

There are two docker compose run configurations

## With Traefik in Docker Swarm

Want to know how to setup a docker swarm? Read: https://blog.knulst.de/docker-swarm-just-create-and-use-it

### 1. Adjust DOCKER_REGISTRY and PRIMARY_DOMAIN (replace with your values)

```shell
export DOCKER_REGISTRY=YOUR_REGISTRY_HERE
export PRIMARY_DOMAIN=f1nalboss.de
```

### 2. Build and Push the image

```shell
docker-compose -f docker-compose.jsdos.yml build
docker-compose -f docker-compose.jsdos.yml push
```

### 3. Add Label to Node within Docker Swarm (replace dummy input)

```shell
export NODE_ID=PUT_IN_NODE_OF_HOST_WHERE_YOU_WANT_TO_DEPLOY
docker node update --label-add gitlab.certs-data=true $NODE_ID
```

### 4. Deploy the stack

```shell
docker stack deploy -c docker-compose.jsdos.yml jsdos
```

### 5. Play

https://js-dos.PRIMARY_DOMAIN

# Run Locally

Use docker-compose to run locally:

```shell
docker-compose -f docker-compose.dev.yml up -d --build
```

# Add/Change Games

1. download zip file and store within this directoy

2. adjust Dockerfile, add following files

```shell
COPY ZIP_OF_GAME .
COPY index.html NAME_OF_GAME.html
RUN sed -i s/GAME_ZIP/\"ZIP_OF_GAME\"/ NAME_OF_GAME.html
RUN sed -i s/GAME_ARGS/\"GAME_EXE_FOUND_IN_ZIP\"/ NAME_OF_GAME.html
```

3. open website choose NAME_OF_GAME.html to start