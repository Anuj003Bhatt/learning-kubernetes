# Docker and Kubernetes Commands
The document contains collection of commands generally used with Docker and Kubernetes. Please note that these commands are UNIX specific.
Optional parameters appear in brackets below. For ease of referece only the widely used parameters are included. For the complete list see the official documentation or use the UNIX command line help.

Operation | Commands
--- | ---
List running processes/containers (Stopped are not included here) | ```bash docker ps ```
List all running processes/containers | ```bash docker ps -a```
List IDs of all running processes/containers | ```bash docker ps -aq```
Running a container (creates new one from image) | ```bash docker run [-p outPort:inPort]  [-d][-it] <Image>```
Starting an existing container | ```bash docker start [-a] <Container>``` 
Attach to a running container | ```bash docker attach <Container>```
Stopping a running container | ```bash docker stop <Container>```
Removing a running process | ```bash docker rm <Container>```
Removing all running processes | ```bash docker rm $(docker ps -aq)```
List Images | ```bash docker images -a```
Delete Image | ```bash docker rmi <Image>```
Delete all Images | ```bash docker image prune```
Fetch container logs | ```bash docker logs [-f] <Container>```

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

