## js-dos in docker
Uses sample pac-man shareware for test.

## add another zip for dosbox

1. download zip file and store within this directoy

2. adjust Dockerfile, add following files

```shell
COPY ZIP_OF_GAME .
COPY index.html NAME_OF_GAME.html
RUN sed -i s/GAME_ZIP/\"ZIP_OF_GAME\"/ NAME_OF_GAME.html
RUN sed -i s/GAME_ARGS/\"GAME_EXE_FOUND_IN_ZIP\"/ NAME_OF_GAME.html
```

3. open website choose NAME_OF_GAME.html to start
