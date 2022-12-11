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

```bash
    cd ./backend
    
    # add mongodb credentials in .env
    cp .env.example .env
    
    # run mongodb container
    docker run --name mongodb --network goals-net --env-file=.env -d --rm -v mongo-volume:/data/db  mongo
    
    # build backend image 
    docker build -t goals-node .

    # run node js backend container
    docker run --name goals-app --network goals-net --env-file=.env -d --rm -p 80:80 -v goals-logs:/app/logs -v "$(pwd):/app" -v /app/node_modules   goals-node

    ###################
    
    cd ../frontend
    
    # build react frontend image
    docker build -t goals-node-frontend .

    # run frontend container
    docker run --name goals-app-frontend --network goals-net --rm -d -p 3000:3000 -it -v "$(pwd):/app" -v /app/node_modules goals-node-frontend

```