### Exercise 2: Changing images.
In this exercise, we'll do how to modify an existing Docker image, and commit it as a new one.
we'll modify the ubuntu:16.04 image to include the ping utility.
### Getting setup:
we use our previous image of ubuntu we pull from docker hub.
### Let's modify an image:
Let's run the image in a new container and install the ping utility.

1.First start the container with /bin/bash:
```
dhruvrajsinh@sf-cpu-371:~ $ docker run -it ubuntu:16.04 /bin/bash
root@786b94c53c6d:/#
```
2. Try running ping in terminal.
3. but it will show that command not found so we have to download ping utility in our system.
4. so first we have to update by apt-get-update
```
root@786b94c53c6d:/# apt-get update
Get:1 http://security.ubuntu.com/ubuntu xenial-security InRelease [102 kB]
Get:2 http://security.ubuntu.com/ubuntu xenial-security/universe Sources [29.6 kB]   
Get:3 http://archive.ubuntu.com/ubuntu xenial InRelease [247 kB]    
Get:4 http://security.ubuntu.com/ubuntu xenial-security/main amd64 Packages [308 kB]
Get:5 http://security.ubuntu.com/ubuntu xenial-security/restricted amd64 Packages [12.8 kB]
Get:6 http://security.ubuntu.com/ubuntu xenial-security/universe amd64 Packages [132 kB]   
Get:7 http://security.ubuntu.com/ubuntu xenial-security/multiverse amd64 Packages [2936 B]
Get:8 http://archive.ubuntu.com/ubuntu xenial-updates InRelease [102 kB]                 
Get:9 http://archive.ubuntu.com/ubuntu xenial-backports InRelease [102 kB]
Get:10 http://archive.ubuntu.com/ubuntu xenial/universe Sources [9802 kB]
Get:11 http://archive.ubuntu.com/ubuntu xenial/main amd64 Packages [1558 kB]
Get:12 http://archive.ubuntu.com/ubuntu xenial/restricted amd64 Packages [14.1 kB]
Get:13 http://archive.ubuntu.com/ubuntu xenial/universe amd64 Packages [9827 kB]
Get:14 http://archive.ubuntu.com/ubuntu xenial/multiverse amd64 Packages [176 kB]
Get:15 http://archive.ubuntu.com/ubuntu xenial-updates/universe Sources [186 kB]
Get:16 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 Packages [652 kB]
```
5. Now we can install the ping command.
```
root@786b94c53c6d:/# apt-get install iputils-ping
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  libffi6 libgmp10 libgnutls-openssl27 libgnutls30 libhogweed4 libidn11 libnettle6 libp11-kit0 libtasn1-6
Suggested packages:
  gnutls-bin
The following NEW packages will be installed:
  iputils-ping libffi6 libgmp10 libgnutls-openssl27 libgnutls30 libhogweed4 libidn11 libnettle6 libp11-kit0 libtasn1-6
0 upgraded, 10 newly installed, 0 to remove and 0 not upgraded.
Need to get 1303 kB of archives.
After this operation, 3778 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
```
6. now we are able to use ping command.
```
root@786b94c53c6d:/# ping google.com
PING google.com (172.217.4.206) 56(84) bytes of data.
64 bytes from lga15s48-in-f14.1e100.net (172.217.4.206): icmp_seq=1 ttl=37 time=0.936 ms
64 bytes from lga15s48-in-f14.1e100.net (172.217.4.206): icmp_seq=2 ttl=37 time=0.367 ms
64 bytes from lga15s48-in-f14.1e100.net (172.217.4.206): icmp_seq=3 ttl=37 time=0.258 ms
^C
--- google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2033ms
rtt min/avg/max/mdev = 0.258/0.520/0.936/0.297 ms
root@786b94c53c6d:/# exit
exit
$
```
### Let's commit changes:
installing ping command everytime is not very special why we can do some that after we pull the images the ping command is already install.
this concept is called docker commit.
1.Let's find our container to create the new image from.

Fortunately, we have a Docker container with our ping utility already installed from the previous steps. It should be stopped right now, but let's find its container ID.
```
docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
786b94c53c6d        ubuntu:16.04        "/bin/bash"         13 minutes ago      Exited (0) 22 seconds ago                       angry_pike
$
```
2.Now let's commit it as a new image.

docker commit takes a container, and allows you to commit its changes as a new image.
```
docker commit --help

Usage:  docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]

Create a new image from a container's changes

Options:
  -a, --author string    Author (e.g., "John Hannibal Smith <hannibal@a-team.com>")
  -c, --change list      Apply Dockerfile instruction to the created image (default [])
      --help             Print usage
  -m, --message string   Commit message
  -p, --pause            Pause container during commit (default true)
$
```
now let's Pass the container ID, an author, commit message, and give it the name <DockerHub username>/ping:
  ```
$ docker commit -a 'Dabhi Dhruvraj' -m 'Added ping utility.' 786 dabhidhruvraj/ping
sha256:78ba830008a61a09f9eae8ca4ead0966ff501457c23df0f635e0651253b3d0e3
$ 
  ```
 now lwt's check by docker images to see our new images.
 ```
  $ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
dabhidhruvraj/ping  latest              78ba830008a6        About a minute ago   159MB
ubuntu              16.04               6a2f32de169d        4 days ago           117MB
$
  ```
  now let's run this new images in new container to show that ping is work or not.
  ```
  $ docker run -it --rm dabhidhruvraj/ping /bin/bash
root@3ab21a456c9f:/# ping google.com
PING google.com (172.217.4.206) 56(84) bytes of data.
64 bytes from lga15s48-in-f14.1e100.net (172.217.4.206): icmp_seq=1 ttl=37 time=1.12 ms
64 bytes from lga15s48-in-f14.1e100.net (172.217.4.206): icmp_seq=2 ttl=37 time=0.380 ms
64 bytes from lga15s48-in-f14.1e100.net (172.217.4.206): icmp_seq=3 ttl=37 time=0.352 ms
^C
--- google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2024ms
rtt min/avg/max/mdev = 0.352/0.620/1.129/0.360 ms
root@3ab21a456c9f:/
  ```
  
  
  





  

