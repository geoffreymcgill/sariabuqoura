## Installation

`https://www.docker.com/products/docker-desktop/` 

- Insure the WSL is running

## Simple Commands

Docker info 

- `docker --version`
- `docker info`

Build the dockerfile 

- `docker build -t new_image_name:v1 .`

list local images 

- `docker images`

Run Docker 

- `docker run -p port-on-host:port-in-container http_get:v1`
- `docker run -p 8080:8080 new_image_name:v1`

Containers

- Running containers
    - `docker ps`
- All containers
    - `docker ps -a`

Logs 

- Logs
    - `docker logs ContainersID`
