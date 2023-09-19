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

