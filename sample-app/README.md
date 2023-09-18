# Sample App to playaround with docker

Sample App to playaround with docker. It includes one API in Node and some packages to be installed. It also has a Dockerfile to build the docker image for this project.

To build the image follow below steps.
- Naviate to the Root of the project. (i.e., where the Dockerfile is present)
- Run the command
```bash
docker build .
```
- This will print the image ID as well on the console.
- To run the image, use below command
```bash
docker run -p 3000:3000 <Image Id>
```
