# THE DOCKER WORKSHOP
## CHAPTER 1 : RUNNING MY FIRST DOCKER CONTAINER

***1.3 Running docker containers***

>**"docker run hello-world"** will help you run your first docker image
```
//step 1
λ docker run hello-world 

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
b8dfde127a29: Pull complete
Digest: sha256:308866a43596e83578c7dfa15e27a73011bdd402185a84c5cd7f32a88b501a24
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
>**"docker ps"** will show you the list of running containers

```
C:\Users\A182503
λ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

```
>**"docker ps -a "** will show you the list of all the containers(running or stopped)

```
λ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
073f171e1f05        hello-world         "/hello"            8 minutes ago       Exited (0) 8 minutes ago                       stupefied_liskov
```
>**"docker images "** will show you the list of all the images(running or stopped)
```
C:\Users\A182503
λ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              d1165f221234        5 days ago          13.3kB
```

***1.4 Managing docker containers***

:arrow_forward: docker pull

:red_circle: docker pull ubuntu:18.04
```
λ docker pull ubuntu:18.04
18.04: Pulling from library/ubuntu
92dc2a97ff99: Pull complete
be13a9d27eb8: Pull complete
c8299583700a: Pull complete
Digest: sha256:4bc3ae6596938cb0d9e5ac51a1152ec9dcac2a1c50829c74abd9c4361e321b26
Status: Downloaded newer image for ubuntu:18.04
docker.io/library/ubuntu:18.04


C:\Users\A182503
λ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              d1165f221234        5 days ago          13.3kB
ubuntu              18.04               329ed837d508        7 days ago          63.3MB
```
:arrow_forward: docker inspect

use the image id to inspect about the image

:red_circle: docker inspect 329ed837d508

```
                                                                                         
  "Id": "sha256:329ed837d5081de117399fa94c258c766c389a9aa21b4013bc0e6444f6e898b0",       
  "RepoTags": [                                                                          
      "ubuntu:18.04"                                                                     
  ],                                                                                     
```
:arrow_forward: docker run -d <image name /image id>

:star: **-d** is used to run the container in detatch mode

```
C:\Users\A182503
λ docker run -d 32
d9d0ca8a0523acec63faac97583afa854a53dcec03df46c22830fe875a261eb9

// as the container starts in the detatch mode it immidiately exits after starting

C:\Users\A182503
λ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
d9d0ca8a0523        32                  "/bin/bash"         33 minutes ago      Exited (0) 33 seconds ago                       fervent_tereshkova
073f171e1f05        hello-world         "/hello"            4 hours ago         Exited (0) 4 hours ago                          stupefied_liskov

```
:star: to keep the container alive we need to use the **-i** and **-t** along with the **-d**

```
C:\Users\A182503
λ docker run -itd 32
64e4a29cdeb4e68d7924a3f8a77add2c35629c5d646b1143ae10c25a722315bc


//now the container is up and running

C:\Users\A182503
λ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
64e4a29cdeb4        32                  "/bin/bash"         32 minutes ago      Up 10 seconds                           gifted_allen
```
:arrow_forward: docker stop <container name /container id> is used to stop a running container

:red_circle: docker stop 64

```
C:\Users\A182503
λ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
64e4a29cdeb4        32                  "/bin/bash"         32 minutes ago      Up 10 seconds                           gifted_allen

//now stop the container

C:\Users\A182503
λ docker stop 64
64
```

:arrow_forward: docker start <container name /container id> is used to start a container

:arrow_forward: docker rm <container name /container id> is used to delete a container

:red_circle: docker rm 64 d9 07

```
C:\Users\A182503
λ docker rm 64 d9 07
64
d9
07

```
:star: if you want to run container and give it a name too then use **--name** tag

:red_circle:**docker run -itd --name ubuntu1 32**

```

C:\Users\A182503
λ docker run -itd --name ubuntu1 32
16c9db3f6bde3cb4fa0b900c4d133efdc1c520434331c0f5f67fa52f963991d7

C:\Users\A182503
λ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
16c9db3f6bde        32                  "/bin/bash"         32 minutes ago      Up 2 minutes                            ubuntu1

```

:star: if you want to run command inside a ubuntu container the we need to use the **docker exec** command.  **"Exec"** helps you access the bash shell .and if you want to start the bash shell then use **/bin/bash**


:red_circle:**docker exec -it 16 /bin/bash**

```

C:\Users\A182503
λ docker exec -it 16 /bin/bash
root@16c9db3f6bde:/#


C:\Users\A182503
λ docker exec -it 16 /bin/bash
root@16c9db3f6bde:/# echo "Hello world from ubuntu1" > hello-world.txt

root@16c9db3f6bde:/# ls
bin  boot  dev  etc  hello-world.txt  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

//now do the cat
root@16c9db3f6bde:/# cat hello-world.txt
Hello world from ubuntu1

//exit to exit the command
root@16c9db3f6bde:/# exit
exit
```
:star: if you want to remove an image then use **docker rmi <image name /image id>**

:red_circle:**docker rmi 32**

```

C:\Users\A182503
λ docker rmi 32
Untagged: ubuntu:18.04
Untagged: ubuntu@sha256:4bc3ae6596938cb0d9e5ac51a1152ec9dcac2a1c50829c74abd9c4361e321b26
Deleted: sha256:329ed837d5081de117399fa94c258c766c389a9aa21b4013bc0e6444f6e898b0
Deleted: sha256:cbcdeed56d9b86e4d36dd5e4e68aae7a8544b9ce13302ba9f29981ea961c5e4a
Deleted: sha256:cff1beb2b6818fbc5e4800231f3558dd7da191e7124bc85d8c45560ed47a31da
Deleted: sha256:837d6facb613e572926fbfe8cd7171ddf5919c1454cf4d5b4e78f3d2a7729000
```

***1.4 Attaching to containers using the attacha commands***

**docker attach** command helps you attach the terminal's standard input output and errors directly to the container . 
In **docker exec** command what we used to do is to get inside the container and the open up the terminal but in **docker attach** it will open the terminal in the primary level.

so if you close the terminal by using the **exit** command then it will stop the container too . so you better use :star:**CTRL+P** followed by :star:**CTRL+Q**
this will help you exit the terminal without closing it .

```
                                                                                                                                          
C:\Users\A182503

// 1. pull the ubuntu image

λ docker pull ubuntu:latest                                                                                                               
latest: Pulling from library/ubuntu                                                                                                       
5d3b2c2d21bb: Pull complete                                                                                                               
3fc2062ea667: Pull complete                                                                                                               
75adf526d75b: Pull complete                                                                                                               
Digest: sha256:b4f9e18267eb98998f6130342baacaeb9553f136142d40959a1b46d6401f0f2b                            
Status: Downloaded newer image for ubuntu:latest  
docker.io/library/ubuntu:latest                                                                                                           
                                                                                                                                          
C:\Users\A182503                                                                                    
//2. get the image list

λ docker images                                                                                                                           
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE                                                      
ubuntu              latest              4dd97cefde62        7 days ago          72.9MB                                                    
//3. run the container                                                                                                  
C:\Users\A182503                                                                                                                          
λ docker run -itd --name ubuntu1 4d                                                                                                       
47f4e6bf47721e63e72f3e01f03cbd16d7d7ce8a4e0033e41ef2f6814be6d8f0                                                                          

//4. check if the container is in running stage or not

C:\Users\A182503                                                                                                                          
λ docker ps                                                                                                                               
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES             
47f4e6bf4772        4d                  "/bin/bash"         23 minutes ago      Up 12 seconds                           ubuntu1           

//5. add docker attach and then safe exit by making sure that the container is still in running stage and then call the exit command to see the difference


C:\Users\A182503                                                                                                                          
λ docker attach 47                                                                                                                        
root@47f4e6bf4772:/# read escape sequence                                                                                                 
                                                                                                                                          
C:\Users\A182503                                                                                                                          
λ docker ps -a                                                                                                                            
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES             
47f4e6bf4772        4d                  "/bin/bash"         23 minutes ago      Up About a minute                       ubuntu1           
                                                                                                                                          
C:\Users\A182503                                                                                                                          
λ docker attach 47                                                                                                                        
root@47f4e6bf4772:/# exit                                                                                                                 
exit                                                                                                                                      
                                                                                                                                          
C:\Users\A182503                                                                                                                          
λ docker ps -a                                                                                                                            
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES     
47f4e6bf4772        4d                  "/bin/bash"         24 minutes ago      Exited (0) 19 seconds ago                       ubuntu1   
                                    
```
:star: if you want to get rid of the unused containers then use  **docker system prune -fa**

```
C:\Users\A182503
λ docker system prune -fa
Deleted Containers:
47f4e6bf47721e63e72f3e01f03cbd16d7d7ce8a4e0033e41ef2f6814be6d8f0

Deleted Images:
untagged: ubuntu:latest
untagged: ubuntu@sha256:b4f9e18267eb98998f6130342baacaeb9553f136142d40959a1b46d6401f0f2b
deleted: sha256:4dd97cefde62cf2d6bcfd8f2c0300a24fbcddbe0ebcd577cc8b420c29106869a
deleted: sha256:95bc1f83306cc7ebaa959492929d6624b0cc1bb6ba61be1cd04fed7d39b002fc
deleted: sha256:a0fcf305193749a4fe8c9da074c4781a0f1e63f2c5b5a979a88597ada5c74645
deleted: sha256:aeb3f02e937406fb402a926ce5cebc7da79b14dbcb4f85a5ce0e3855623cec80

Total reclaimed space: 72.9MB

C:\Users\A182503
λ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

### EXERCISE
:grey_question: Create a Postgres database container instance that will serve as the data tier of our application stack.Use environment variables to configure the container at runtime to use the following database credentials:
> username: panoramic password: trekking
>>Expected output 
>>> CONTAINER ID  IMAGE         COMMAND                 CREATED
  STATUS              PORTS               NAMES
  >>>>29f115af8cdd  postgres:12   "docker-entrypoint.s…"  4 seconds ago
  Up 2 seconds        5432/tcp            blissful_kapitsa
  
:point_right:

> To start the Postgres Docker container, first determine what environment variables are required to set the default username and password credentials for the database. Reading through the official Docker Hub page, you can see that you have configuration options for the POSTGRES_USER and POSTGRES_PASSWORD environment variables. Pass the environment variables using the -e flag. The final command to start our Postgres Docker container will be as follows:

> docker run -itd -e "POSTGRES_USER=panoramic" -e "POSTGRES_PASSWORD=trekking" postgres:12

:grey_question: Activity 1.02: Accessing the Panoramic Trekking App Database
> Log in to the Postgres database container using the PSQL command-line utility.
Once logged in to the database, return a list of databases in Postgres by default.
Note

>If you are not familiar with the PSQL CLI, the following is a list of reference commands to assist you with this activity:

>Logging in: psql --username username --password

>Listing the database: \l

>Quitting the PSQL shell: \q

:point_right:

```
//first log in 
docker exec -it <containerID> psql --username panoramic --password

// "\l" to display list of database

C:\Users\A182503
λ docker exec -it d2 psql --username panoramic --password
Password:
psql (12.6 (Debian 12.6-1.pgdg100+1))
Type "help" for help.

panoramic=# \l
                                  List of databases
   Name    |   Owner   | Encoding |  Collate   |   Ctype    |    Access privileges
-----------+-----------+----------+------------+------------+-------------------------
 panoramic | panoramic | UTF8     | en_US.utf8 | en_US.utf8 |
 postgres  | panoramic | UTF8     | en_US.utf8 | en_US.utf8 |
 template0 | panoramic | UTF8     | en_US.utf8 | en_US.utf8 | =c/panoramic           +
           |           |          |            |            | panoramic=CTc/panoramic
 template1 | panoramic | UTF8     | en_US.utf8 | en_US.utf8 | =c/panoramic           +
           |           |          |            |            | panoramic=CTc/panoramic
(4 rows)

panoramic=#
 // exit using "\q"
 
panoramic=# \q
```


**XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXChapter 1 Completed XXXXXXXXXXXXXXXXXXXXXXXXXX**

## CHAPTER 2 : GETTING STARTED WITH DOCKER FILES
### DOCKER FILE

:star: if you want to add comment to dockerfile then use **#**

:red_circle:**# this is a comment**

```
# This is a comment
DIRECTIVE argument
```

### COMMON DIRECTIVES IN DOCKERFILE
These are few common directives
1. FROM
2. LABEL
3. RUN
4. CMD
5. ENTRYPOINT

***
**1. FROM** DIRECTIVE
***
1. A Dockerfile usually starts with the FROM directive. 
2. This is used to specify the parent image of our custom Docker image. 
    a. The parent image is the starting point of our custom Docker image. 
    b. All the customization that we do will be applied on top of the parent image. The parent image can be an image from Docker Hub, such as Ubuntu, CentOS, Nginx, and MySQL. 
    
 3. The FROM directive takes a valid image name and a tag as arguments. If the tag is not specified, the latest tag will be used.

:red_circle:**SYNTAX image:tag**

```
FROM ubuntu:20.04
```
Additionally, we can use the base image if we need to build a Docker image from scratch. The base image, known as the **scratch** image, is an empty image mostly used to build other parent images.

In the following ***FROM*** directive, we are using the scratch image to build our custom Docker image from scratch:

```
FROM scratch
```
***
**2. LABEL** DIRECTIVE
***

1. A LABEL is a key-value pair that can be used to add metadata to a Docker image. 

2. These labels can be used to organize the Docker images properly. An example would be to add the name of the author of the Dockerfile or the version of the Dockerfile.

A LABEL directive has the following format:

:red_circle: **SYNTAX key = value**

if you want to view labels then try **docker image inspect image-id**

```

LABEL maintainer=sathsara@mydomain.com
LABEL version=1.0
LABEL environment=dev

or you can write it like so 

LABEL maintainer=sathsara@mydomain.com version=1.0 environment=dev

```
***
**3. RUN** DIRECTIVE
***

1. Run directive is used to execute command during the **image build time**. 

2. This will create a new layer on top of the existing layer, execute the specified command, and commit the results to the newly created layer. 

3. The RUN directive can be used to install the required packages, update the packages, create users and groups, and so on.

4. A docker file can have multiple RUN directive .


The RUN directive takes the following format:

:red_circle: **RUN command**

```
RUN apt-get update
RUN apt-get install nginx -y

 or you can write as 
 
 RUN apt-get update && apt-get install nginx -y
```

***
**4. CMD** DIRECTIVE
***

1. A Docker container is normally expected to run one process. A CMD directive is used to provide this default initialization command that will be **executed when a container is created from the Docker image**.

2. A Docker file can execute only one CMD directive. 

3. If there is more than one CMD directive in the Dockerfile, Docker will execute only the last one.

```
CMD ["executable","param1","param2","param3", ...]

CMD ["echo","Hello World"]

$ docker container run <image>
Hello World


```

***
**5. ENTRYPOINT** DIRECTIVE
***

1. Similar to the CMD directive, the ENTRYPOINT directive is also used to provide this default initialization command that will be executed when a container is created from the Docker image. 

2. The difference between the CMD directive and the ENTRYPOINT directive is that, unlike the CMD directive, we cannot override the ENTRYPOINT command using the command-line parameters sent with the docker container run command.

> **The --entrypoint flag can be sent with the docker container run command to override the default ENTRYPOINT of the image.**

```

# This is my first Docker image
FROM ubuntu 
LABEL maintainer=sathsara@mydomain.com 
RUN apt-get update
CMD ["The Docker Workshop"]
ENTRYPOINT ["echo", "You are reading"]
```

### Building Docker Images

lets try to build the docker image from the above mentioned Dockerfile .

if Docker image is a class then container is the object .

> **All the layers in the Docker image are read only** .
>
> Once we create the container from the image, a new writable layer is created on top of the existing layer .


To build a docker image we need to run the below command inside the directory where we have created the Dockefile .

:red_circle: **SYNTAX** docker image build context

```shell
docker image build <context>

// to run the docker file that we have 
C:\DEV\practice\DockerFinal (master)
λ ls
custom-docker-image/  dockerpractice.md

C:\DEV\practice\DockerFinal (master)
λ cd custom-docker-image\

C:\DEV\practice\DockerFinal\custom-docker-image (master)
λ ls
Dockerfile

C:\DEV\practice\DockerFinal\custom-docker-image (master)
λ docker build .
[+] Building 98.4s (6/6) FINISHED
 => [internal] load build definition from Dockerfile 
 
Use 'docker scan' to run Snyk tests against images to find vulnerabilities and learn how to fix them

```

now if we try to see images, we can see below

```bash
C:\DEV\practice\DockerFinal\custom-docker-image (master)
λ docker images
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
<none>       <none>    9bb746264d02   3 minutes ago   103MB
ubuntu       latest    fb52e22af1b0   10 hours ago    72.8MB
```
we can see that the images have no tag name and Repository name .

lets add it .

```bash
C:\DEV\practice\DockerFinal\custom-docker-image (master)
λ docker image tag 9bb myfirstimage:1.0

C:\DEV\practice\DockerFinal\custom-docker-image (master)
λ docker images
REPOSITORY     TAG       IMAGE ID       CREATED          SIZE
myfirstimage   1.0       9bb746264d02   12 minutes ago   103MB
ubuntu         latest    fb52e22af1b0   10 hours ago     72.8MB

```




