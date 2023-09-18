# Docker and Kubernetes Commands
The document contains collection of commands generally used with Docker and Kubernetes. Please note that these commands are UNIX specific.
Optional parameters appear in brackets below. For ease of referece only the widely used parameters are included. For the complete list see the official documentation or use the UNIX command line help.

Operation | Commands
--- | ---
List running processes/containers (Stopped are not included here) | ```bash docker ps ```
List all running processes/containers | ```bash docker ps -a```
List IDs of all running processes/containers | ```bash docker ps -aq```
Running a container | ```bash docker run [-p outPort:inPort] <Image ID>```
Stopping a running container | ```bash docker stop <Container ID>```
Removing a running process | ```bash docker rm <Container ID>```
Removing all running processes | ```bash docker rm $(docker ps -aq)```
List Images | ```bash docker images -a```
Delete Image | ```bash docker rmi <Image ID>```
Delete all Images | ```bash docker rmi $(docker images -aq)```
