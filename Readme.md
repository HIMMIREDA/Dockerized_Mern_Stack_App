# Dockerizing a MERN stack app using docker

## Features

### mongodb :

1. data is persistent using volumes
2. database access is limited using username and password

### Backend

1. Logs data is persistent using volumes
2. Live source code update using bind mounts and nodemon

### Frontend

1. Live source code update

## How to run

### 1. using docker cli:

```bash
    cd ./backend

    # add mongodb credentials in .env
    cp .env.example .env

    # run mongodb container
    docker run --name mongodb --network goals-net --env-file=.env -d --rm -v mongo-volume:/data/db  mongo

    # build backend image
    docker build -t goals-node-backend .

    # run node js backend container
    docker run --name goals-app-backend --network goals-net --env-file=.env -d --rm -p 80:80 -v goals-logs:/app/logs -v "$(pwd):/app" -v /app/node_modules goals-node-backend

    ###################

    cd ../frontend

    # build react frontend image
    docker build -t goals-node-frontend .

    # run frontend container
    docker run --name goals-app-frontend --rm -d -p 3000:3000 -it -v "$(pwd)/src:/app/src" -v /app/node_modules goals-node-frontend

```

### 2. using docker compose:

```bash
docker-compose up -d # running containers
```

```bash
    docker-compose down # if you want to stop containers and delete them (persist data volumes)
```

```bash
    docker-compose down -v # if you want to stop and delete containers and volumes
```
