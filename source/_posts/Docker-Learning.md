---
title: Docker Learning
mathjax: true
date: 2020-09-17 13:43:39
tags:
categories:
---

# Preview

***



This semester, I was going to do some project such as machine learning, MIT 6.828 course, on my Raspberry Pi. So, I obsessed to learn the using of docker.



This blog continues to be updated.



# Basic Ideas

***

Raspberry pi 4 is based on **ARM** architecture, and Docker CE not only support **x86_64**, but also **ARM**. So to suit for docker CE, your raspberry pi's OS should be **Raspberry Pi OS Buster**



There are two different ways to install docker on your PC.



# Installation 

***

Thanks for [this blog](https://yeasy.gitbook.io/docker_practice/install/raspberry-pi), most of the installation part of Docker on Raspberry pi is based on this blog.



## Using Shell Script

***

 Actually, for the guys like me, just for learning docker and blahblahblah, I highly recommended you to use this method, maybe after plenty of experience of docker, you can use **apt** method which will be introduced next chapter.

```shell
$ curl -fsSL get.docker.com -o get-docker.sh && sudo sh get-docker.sh --mirror Aliyun
```



The option *mirror* will determine whether to use mirror source to speed up the downloading process. Because some country may have some problem on connecting with its official website.



## Apt method

***

First step, adding some packages using HTTPS and CA certification

```shell
$ sudo apt-get update

$ sudo apt-get install \
     apt-transport-https \
     ca-certificates \
     curl \
     gnupg2 \
     lsb-release \
     software-properties-common
```



Now, to confirm the legality of the software you wanna download, add GPG key

```shell
$ curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/raspbian/gpg | sudo apt-key add -


# official
# $ curl -fsSL https://download.docker.com/linux/raspbian/gpg | sudo apt-key add -
```



Now, we need to add the source of Docker CE software:

```shell
$ sudo add-apt-repository \
    "deb [arch=armhf] https://mirrors.ustc.edu.cn/docker-ce/linux/raspbian \
    $(lsb_release -cs) \
    stable"


# official
# $ sudo add-apt-repository \
#    "deb [arch=armhf] https://download.docker.com/linux/raspbian \
#    $(lsb_release -cs) \
#    stable"
```

Ensure you have accomplish the step 1, otherwise you may not use ``add-apt-repository``

The last step, load the elephant into the refrigerator.

```shell
$ sudo apt-get update

$ sudo apt-get install docker-ce
```





# Launch the Docker

***

If you OS use ``systemd``(actually the system that blog recommended is using ``systemd``), run this command

```shell
$ sudo systemctl enable docker
$ sudo systemctl start docker
```



Now, we gonna create a group named ``docker`` , and add your current user into docker so that without  becoming ``root`` user can you use docker.

```shell
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
# For instance, maybe you are still login your raspberry pi as user, normally, pi, you can use pi to replace `$USER`: `sudo usermod -aG docker pi`
```



## Test The Installation

***

Try this:

```shell
$ docker run arm32v7/hello-world

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
d1725b59e92d: Pull complete
Digest: sha256:0add3ace90ecb4adbf7777e9aacf18357296e799f81cabc9fde470971e499788
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



Maybe you will meet with this situation, which is the situation I've met at the first installation:

```shell
Docker: Error response from daemon: failed to create endpoint on network bridge: failed to add blahblahblah....
```



Try to reboot your raspberry ;). Maybe it also works for you.



## Speed Up

***

As I've mentioned, many country may have some problem with contacting with the hub of docker. For linux using `systemd`, such as Ubuntu 16.04+、Debian 8+、CentOS 7.



Find `/etc/docker/daemon.json` (if this file doesn't exist, create it), and adding the contents like this:

```json
{
  "registry-mirrors": [
    "https://hub-mirror.c.163.com",
    "https://mirror.baidubce.com"
  ]
}
```

Always remember this must be strictly satisfy with the `json` format.



Then restart the service:

```shell
$ sudo systemctl daemon-reload
$ sudo systemctl restart docker
```



# Basic Usage

***

About the usage tutorial of docker, there is no doubt that the official docs are the best choice. And for most people who just try to use some frequently used docker command, I highly recommend [this blog](https://yeasy.gitbook.io/docker_practice/install/raspberry-pi) which I've mentioned before.



## Basic Idea

***

There are some basic concepts of docker, such as image, container and repository. And just keep in mind the following points will just be fine. To explore more, you can read the blog I recommend and search in the docs.

* Always keep in mind, the more specifically usage of the command can be learnt from docs or ``--help``

* The image is composed by a set of files which are organized by hierarchy architecture.
* The changes you've done on container will just be record into the current storage file.
* It's funny that docker actually working in a C/S mode. That create a **context** concept. The process of creating your own image will be done on docker's **'server'**, and the range of files that you can manipulate is determined by the **context**. More specifically, only the files under the **context** directory.
* To save the space, docker rely on the mechanism which the file is multi-used. 



## Basic Image Operation

***

* Get the image: ``docker pull [opts] RepositoryName[:tag]`` 
* list the image: ``docker image ls [opts] [repository[:tag]]``
  * ``-f``(also named ``--filter``) is quite useful, according to that blog.
  * The combination of ``-f`` and ``-q`` will just the ID of the dockers that you wanna remove.
* remove the image: ``docker image rm [opts]  <Image id list>`` or ``docker rmi [opts] <Image id list>``
  * Remember that, you can only remove the certain image when there is no other container is based on it.
  * The things really happens when we run the remove commands, is well interpreted in the blog. Broadly speaking, it has *untagged* process and *Deleted* process.
  * ``docker container prune``: this will remove all the unused images. 



## Container Operation

***



### Running Docker

***

* command format: ``docker run [opts] repository:tag [CMD]``
  * ``[CMD]`` represent the first command executed by docker when you first create a brand new docker. Otherwise, without this, it will be determined by docker file
* ``-i``: Interactive mode, keep container's stdin open
* ``-t``: Dispatch a pseudo-tty binding with stdin
* ``--rm``: Once you stop the container, it will be removed automatically.
* ``-d``: Docker will execute its command at background. You can check the output by ``docker container logs``



### Start, Restart and Stop

***



* ``docker container stop``: Stop the container. In the interactive mode, you can also achieve this by  ``exit`` or <kbd>ctrl</kbd>+<kbd>d</kbd>
* ``docker restart``: used to stop the container that is running and restart it
* ``docker start``: start the container which is in the terminate mode



### Enter the Container

***

This is aimed to handle the container which is running with ``-d``, there are two commands: ``attach`` and ``exec``

* ``docker attach``: If you  use ``exit``, the container will stop
* ``docker exec [OPOTIONS] CONTAINER COMMAND [ARG]``: Can be followed by ``-i``, ``-t``. When you exit, the container will not stop.



### Remove

***

* ``docker container rm ``: Remove a container which is in the terminate mode
  * ``-f``: with this options, you can remove a container in the running mode
* ``docker prune``: Remove all the containers that is in the terminate mode



### Commit



 Actually, you can create your own image in this way. However, it's not a recommended method. Because of hierarchy architecture that I've mentioned before, this will cause unnecessary redundant on **image**, such as you can't predict what will really happen when you use remove commands to build your image. It's also troublesome that it is really hard to maintain because it's hard to assure what happened about this new image. What's more, the logical design of this way can't be explained in an explicit way. 

However, just like what said in the reference blog, use commit we can easily comprehend the mechanism about how **dockerfile** create your own image and what will happen when docker is creating an image refer to **dockerfile**.

Firstly, you create a container use the image that you already have. Do some operation on it and make some change. You can check the difference caused by your operation by ``docker diff``. 

Then the leading actor of this section ``commit`` will show us its function. 

``docker commit [opt] <container's ID or name> [repository name[: tag]]`` 

Use the container modified by you to create a new image which is especially identified by ``[repository name[: tag]]``. 

You can use ``docker history`` to see the logs recording the process of creating this image. Actually, it also shows the layers which compose this image. When you try to use this image to create a new container and run it, you will feel that it seems that you've already done the operation, which you've done on the original operation before, on this container too. 



## Dockerfile

***

Using **Dockerfile** is more formal way to build an image. Suppose we've already finish a Dockerfile. How to best use it to create a demo image?

The answer is ``docker build``, we can use this command to build an image from a Dockerfile. Usage: ``docker build [OPTIONS] PATH | URL | -`` . 

Default Dockerfile path this command utilize to built an image is the current working directory. You can also point out the path for docker with option ``-f``.

``-t`` is also a useful option, you can  name and choose a tag in the ``repository name:tag`` format.

More details can be checked by ``--help``. Let's focus on something that is more challenging about this process. 

### Context

***

As I've mentioned before, context is an important concept when we building a new image. Because docker use ``client-server`` structure to achieve the task. So the first job when docker is creating a new image is confirm the content of context on the docker's server. More specifically, docker's client will copy all the files under the ``PATH`` you've sent to the docker's server. After that, docker's server will set it as "working directory".

All the local materials that you need to create a new image should be under that ``PATH``. For example, maybe in your Dockerfile, there exists some instruction such as ``COPY``, ``ADD``, which are using local files to create your docker's image. Then, those file should be contained under the ``PATH`` you give.



### Syntax Of Dockerfile's  Basic Instruction

***

* Rule of thumb: One instruction will build one layer. It's the guideline of building current layer.
* ``FROM``: This point out the basic image we used for docker.
  * There are plenty of high-quality official images on dockerhub.
  * For server's image: ``nginx, redis, mongo, mysql, httpd`` and etc
  * More basic, you can also choose those OS image: ``ubuntu, debian, centos``
  * A special image ``scratch``: actually, ``From scratch`` doesn't set any image as a base, this is a virtual concept which represent no image base.
* ``RUN``: One of the most common used commands, it will automatically run the commands after it during the creating image process.
  * There are two format: *shell* format and *exec* format
  * *shell* format: ``RUN <commands>``
  * *exec* format: ``RUN ["EXEC FILE", "OPT1", "OPT2", ...]``, it looks like you're using a function.
  * Like I've mentioned in rule of thumb, one instruction is correspond to a layer. You need to think really carefully what commands should be added after the ``RUN``.  Using ``&&``, `` ||`` , ``;`` and ``\`` , which is based on the syntax feature of shell commands, is a good strategy to organize the commands used to build image.
  * ``#`` at the head of line is used to take notes.
* ``WORKDIR``: Appoint the working directory. The operation contained by instructions, which are after  ``WORKDIR`` instruction, will work at the working directory appointed by ``WORKDIR``.
  * [Reference Blogs](https://yeasy.gitbook.io/docker_practice/image/dockerfile/workdir) points out an interesting fact by an example of improper using . Like I've said, every instruction will create a container, complete the operations, commit it and add it as a new layer. So when you use next instruction, the working directory has nothing to do with the final working directory in the former container created by  previous  instruction. It will only be initialized by ``WORKDIR``.
  * If ``WORKDIR`` use relative path to set the  later working directory, the path it switched is related to the previous ``WORKDIR``.
* ``CMD``: 

### Example

***

Here is an example. My original reason of learning docker is try to learn MIT 6.828 course. I wanna run this lab on my docker. So I created a dockerfile:

```dockerfile
FROM ubuntu:16.04

RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak  \
    && cat << _EOF_ >> /etc/apt/sources.list
# My Source
# TsingHua
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse

# Ali
deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
_EOF_
RUN apt-get update \
    && apt-get --no-install-recommends install -y gcc make build-essential gdb gcc-multilib zlib1g-dev libglib2.0-dev libpixman-1-dev
RUN apt-get install -y git \
    && git clone https://github.com/mit-pdos/6.828-qemu.git qemu \
    && git clone https://pdos.csail.mit.edu/6.828/2018/jos.git mit_lab_os \
    && apt-get remove -y git
RUN cd qemu \
    && ./configure --disable-kvm --target-list="i386-softmmu x86_64-softmmu" \
    && make \
    && make install \
    && cd .. \
    && rm -rf qemu

WORKDIR "/mit_lab_os"

CMD ["bash"]
```

