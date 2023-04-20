### Exercise 3: Building new images:
in this exercise we will do how to create a new Docker image.
In this exercise i have already a simple react project in my system so let's build the image for this project.

### Creating a Docker-file.
for building a images we must have to make a dockerfile and run that dockerfile to build a images.
The Dockerfile is a "recipe" of sorts, that contains a list of instructions on how to build a new image.
let's create a dockerfile.
```
$ touch Dockerfile
```
inside the dockerfile we have to provide this.
```
FROM node                  # Use the official Node.js image as the base image
WORKDIR /app/src           # Set the working directory to /app/src
COPY package.json .        # Copy package.json from the current directory to /app/src
COPY package-lock.json .   # Copy package-lock.json from the current directory to /app/src
RUN npm install            # Install dependencies defined in package.json
COPY . .                   # Copy the current directory (all files) to /app/src
EXPOSE 3000                # Expose port 3000 to allow connections to the container
CMD ["npm", "start"]       # start the application with npm
```
finally we create our dockerfile.
### Building a dockerfile.
to build docker images from dockerfile we use docker build command. The docker build command reads a Dockerfile, and runs its instructions to create a new image.
```
$ docker build -t dabhidhruvraj/react .
```
here dabhidhruvraj/react is our image name and . pointed that we want docker image in this directory.
running docker images we can see our new image.
```
dhruvrajsinh@sf-cpu-371:~$ docker images
REPOSITORY                               TAG         IMAGE ID       CREATED         SIZE
node_crud_server                         latest      8341dfd54ef4   25 hours ago    1.01GB
node_crud_client                         latest      7e60920f7dee   5 days ago      746MB
exercise-image                           version_1   a168c8879468   6 days ago      1GB
dabhidhruvraj/trainee-practical-devops   latest      a168c8879468   6 days ago      1GB
node_crud_db                             latest      9f6d0d222a47   7 days ago      496MB
my_db                                    latest      90bafe543c3d   7 days ago      496MB
mysql                                    latest      412b8cc72e4a   13 days ago     531MB
ubuntu                                   latest      08d22c0ceb15   6 weeks ago     77.8MB
```
