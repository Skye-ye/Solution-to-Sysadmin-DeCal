# Solution to Lab10a

## Intro to Docker

1. "root"

2. No, it's not the same because their hash is not the same.
## Basic Management

1. I found that I entered the python interactive mode when I ran `docker run -it mypython` command.

2. ```dockerfile
   FROM ubuntu:bionic
   
   RUN apt-get update && apt-get install -y fortune fortunes-min
   
   CMD ["/usr/games/fortune"]
   ```

3. ```
   REPOSITORY                TAG       IMAGE ID       CREATED          SIZE
   myfortune                 latest    4ab7fc53f760   3 minutes ago    112MB
   mypython                  latest    2725fa378db7   13 minutes ago   139MB
   ```

## Dungeons and docker-compose

`Dockerfile`:

```dockerfile
FROM ubuntu:xenial

RUN apt-get update && \
    apt-get install -y nodejs npm netcat

WORKDIR /app

COPY ./decal-sp18-a10 /app

RUN npm install

EXPOSE 8080

CMD ["./wait-for", "database:27017", "--timeout=30", "--", "nodejs", "server.js"]
```

`docker-compose.yml`:

```dockerfile
version: '3'
services:
  web:
    build: .
    ports:
      - "8080:8080"
    depends_on:
      - database

  database:
    image: mongo:latest
    ports:
      - "27017:27017"
```







