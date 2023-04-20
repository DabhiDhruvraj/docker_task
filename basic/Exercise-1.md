## Exercise_1: running container
when we want to run a particular container we have to pull the image.
## pulling an image 

1. what images we have currently on our machine by running docker images
```
$ docker images
```

2. let's pull the images from dockerhub by using the docker pull command. we want the image of ubuntu.
```
$ docker pull ubuntu:16:04
```
3. here 16:04 is a specific version of ubuntu images and we can also pull different version on the same image.
4. After this we can run docker images to see our images is pulling down or not 
```
$ docker images
REPOSITORY                               TAG         IMAGE ID       CREATED         SIZE
node_crud_server                         latest      8341dfd54ef4   24 hours ago    1.01GB
node_crud_client                         latest      7e60920f7dee   5 days ago      746MB
dabhidhruvraj/trainee-practical-devops   latest      a168c8879468   6 days ago      1GB
exercise-image                           version_1   a168c8879468   6 days ago      1GB
node_crud_db                             latest      9f6d0d222a47   7 days ago      496MB
my_db                                    latest      90bafe543c3d   7 days ago      496MB
mysql                                    latest      412b8cc72e4a   13 days ago     531MB
ubuntu                                   latest      08d22c0ceb15   6 weeks ago     77.8MB
```
### Removing images:
5. okk now we want to delete or remove this images so we can do that by using docker rmi command then provide a id of that images or name of that images.
```
$ docker rmi 08d22
or
$ docker rmi ubuntu
```
### running a container:
7. now we pull the images of ubuntu let's run our first container by using docker run command.
```
$ docker run ubuntu:16.04
```
8. here we don't mentioned a name of container so docker create a random name for that container but if we want to give name by ourself we can do that by --name
```
$ docker run --name dhruvraj ubuntu:16.04
```
9. we can check the list of containers by typing docker ps command.
```
$ docker ps
```
10.we can also see the previous container or stopped container by typing docker ps -a command.
```
$ docker ps -a
CONTAINER ID   IMAGE          COMMAND       CREATED        STATUS                    PORTS     NAMES
c2f18885e798   ubuntu:16.04   "/bin/bash"   19 hours ago   Exited (0) 19 hours ago             hello
```
11. also we can run the container in interactively mode by providing -it.
```
$ docker run -it ubuntu:16.04
```
12 let's see what happened.
```
root@5fa68739793c:/# pwd
/
root@5fa68739793c:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```
13. If we want to exit from this container provide exit.
```
root@5fa68739793c:/# exit
exit
```
By default our terminal remains attached to the container when you run docker run. What if you don't want to remain attached?

By adding the -d flag, we can run in detached mode, meaning the container will continue to run as long as the command is, but it won't print the output.
```
$ docker run -d ubuntu:16.04 /bin/sleep 3600
be730b8c554b69383f30f71222b9ac264367c7454790dc2a4eb0cda33c0baa2a
$
```
14. Let's use docker stop, passing it the first few characters of the container name we want to stop.
```
$ docker stop <container id or name>
```
15. again typing docker ps -a to see our container is stopped or not.
```
$ docker ps -a
```



