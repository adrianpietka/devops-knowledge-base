# Docker

## Containers

```bash
docker ps

docker rm -f [container id]
docker rm $(docker ps -aq)

docker exec -i [container id] [command]
docker exec -i f3b //bin/bash

docker run -it [container id] [command]
docker run -it [container id] /bin/bash

docker port [container id]

docker top [container id]
```

## Images

```bash
docker images

docker build -t image-name .

docker rmi image-name
docker rmi $(docker images -aq) -f
```
