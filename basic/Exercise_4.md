### Exercise 4: Sharing Images
in this exercise we will learn how to share docker images using dockerhub. it is a great place to find images and upload our own images to.
For this exercise we see that which images we have in our system.
```
dhruvrajsinh@sf-cpu-371:~$ docker images
REPOSITORY                               TAG         IMAGE ID       CREATED         SIZE
node_crud_server                         latest      8341dfd54ef4   27 hours ago    1.01GB
node_crud_client                         latest      7e60920f7dee   5 days ago      746MB
dabhidhruvraj/trainee-practical-devops   latest      a168c8879468   6 days ago      1GB
exercise-image                           version_1   a168c8879468   6 days ago      1GB
node_crud_db                             latest      9f6d0d222a47   7 days ago      496MB
my_db                                    latest      90bafe543c3d   7 days ago      496MB
mysql                                    latest      412b8cc72e4a   13 days ago     531MB
ubuntu                                   latest      08d22c0ceb15   6 weeks ago     77.8MB
ubuntu                                   16.04       b6f507652425   19 months ago   135MB
```
let's push our image dabhidhruvraj/trainee-practical-devops to dockerhub.
ok so let's first login in dockerhub by our username and password.
after that you see the repositry button at the top click on that.
then give our repositry name to our image name.
After that press create button and make sure that your repositry is public.
### push the images.
for pushing our images to remote we use docker push command with tag.
```
dhruvrajsinh@sf-cpu-371:~$ docker push dabhidhruvraj/trainee-practical-devops:version-1
```
finally we push our images to dockerhub and we can see that in repositries section.
### Searching images
we can serach the images by typing docker search command.
```
dhruvrajsinh@sf-cpu-371:~$ docker search redis
```

