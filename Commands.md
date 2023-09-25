# Docker and Kubernetes Commands
The document contains collection of commands generally used with Docker and Kubernetes. Please note that these commands are UNIX specific.
Optional parameters appear in brackets below. For ease of referece only the widely used parameters are included. For the complete list see the official documentation or use the UNIX command line help.

Operation | Commands
--- | ---
List running processes/containers (Stopped are not included here) | ```docker ps ```
List all running processes/containers | ```docker ps -a```
List IDs of all running processes/containers | ```docker ps -aq```
Running a container (creates new one from image) | ```docker run [-p outPort:inPort]  [-d][-it][--rm] <Image>```
Starting an existing container | ```docker start [-a] <Container>``` 
Attach to a running container | ```docker attach <Container>```
Stopping a running container | ```docker stop <Container>```
Removing a running process | ```docker rm <Container>```
Removing all running processes | ```docker rm $(docker ps -aq)```
List Images | ```docker images -a```
Delete Image | ```docker rmi <Image>```
Delete all Images | ```docker image prune```
Fetch container logs | ```docker logs [-f] <Container>```
Build a docker image | ```docker build [-t 'name:tag'] <Path To Dockerfile DIR>```

## Parameters explained
Option | Command | Meaning
--- | --- | ---
`-p` | Run Container | Mention the port to run the container on and the port to bind to internally.
`-i` | Run Container | Launch/Expose interactive session.
`-t` | Run/Start container | Launch a pseudo pseudo TTY session
`-d` | Run Container | Detached mode
`-f` | Logs |  Follow
`-a` | Start Container | Start a container in attach mode
`-a` | List processes / Container | Show all (including stopped containers)
`--rm` | Run container | This option removes container automatically once stopped

## Volumes and Bind Mounts
Types of volumes and their use cases:
Anonymous Volumes | Named Volumes | Bind Mounts
--- | --- | ---
Managed by docker | Managed by docker | Manged by Host file system
Created for specific container | Created in general and not for a single container | Location on host file system directly mapped inside the container
Deleted once the container is removed (Note: The volume will survive if the container is stopped only and not removed.) | **NOT** deleted if the container is removed | **NOT** deleted if the container is removed
Since this is anonymous and tied to single container, it cannot be used to share data across containers | Can be used to share data across containers | Can be used to share data across containers
Example: `docker run -v volName:/app/vol1` | Example: `docker run -v volName:/app/vol1` | Example: `docker run -v /users/username/git/project:/app/vol1` (The path `/users/username/git/project` is just an example to show that it is a path from the host system itself.)

## Networking with Containers

### Connecing to Host
- Instead of `localhost` use `host.docker.internal` (This represents host IP)

### Connecing to Other container
You can get the IP of container with the following command.
```bash
docker container inspect <Container>
```
The IP can be found under "Network Settings" in the response.

Although this approach works but always getting the IP and changing the code is not a good approach.
To address this, networks come to the rescue.
- Add the containers under the same network using `--network` option
- Within a network containers can communicate with each other and the IPs are automatically resolved.

To create a network use the below command
```bash
docker network create <Network Name>
```

And then run container using the network option like below
```bash
docker run --name <Container Name> --network <Network Name> <image>
```

To access this container from other containers just use the container name directly instead of `localhost` or `host.docker.internal`.

To get help regarding the command run:
```bash
docker network --help
```

## Docker Compose 
Docker compose is an elegant tool for creating and managing multi-container applications. It is based on one configuration file i.e., `docker-compose.yml` (`docker-compose.yaml` is also fine. YAML and YML both are same).

A sample of docker-compose file is pasted below:
```yaml
services:
  database:
    image: 'mongo'
    volumes:
      - namedVol:/data/db
    environment: # Can be specified using below 2 formats
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: root
      #- MONGO_INITDB_ROOT_USERNAME=root
      #- MONGO_INITDB_ROOT_PASSWORD=root
    # env_file: # Environment variables can also be loaded from a file
      # - ./env/file # This is the relative path from the docker-compose file
  service1: # The above is a pre-built image, docker compose can also build images using the build configuration. Just mention the path to the specific dockerfile path
    build: ./pathToFolderWhereDockerfileIsPresent
    ports:
      - '8080:8080' # Format is 'Host Port: Internal Port'
    volumes:
      - /app/annonymousVolume
      - logs:/app/logs
      - '<Path relative to docker compose for bind mount>':'<Path to bind in container>'
  service2: # There is a detailed object way to build the image as well
    build:
      context: ./pathToFolderWhereDockerfileIsPresent
      dockerfile: <Dockerfile Name> # Note here that with this docker compose it is not necessary to keep the name of the docker file as Dockerfile.
      args:
        some-args: arg-value

volumes:
  namedVol:
  logs:
```

### Notes
- Docker compose by default creates a network and adds the container to that network
- It by default runs containers with `--rm` option.
- To run containers in detached mode use `-d` with docker compose up command. i.e., `docker-compose up -d`
  

# References
- Docker Docs: https://docs.docker.com/
- Docker Compose file: https://docs.docker.com/compose/compose-file/

