---
title: Raspberry Pi Learning
mathjax: true
date: 2020-09-19 00:38:01
tags:	
	- Tools
	- Technique
categories: Raspberry pi
---

# Preview

***



Here record the learning process of my RaspberryPi.



# Search the IP Address of Raspberry PI

***

Because of the lack of screen, I turn to add an empty ssh file in raspberry pi's boot. In order to get access to raspberry pi by ssh. I have to search the IP address first. Here is my way:

```shell
ping raspberrypi.local
```





# About SSH

***

Recently, I learnt that windows terminal it has built-in `ssh` function.  So I took a try on this instead of using PuTTY. However, there are some trouble striking me that.

Firstly, what does this situation means: [ssh: The authenticity of host can't be established](https://superuser.com/questions/421074/ssh-the-authenticity-of-host-host-cant-be-established/421084#421084) . This is **not an error**, it's just **warning** you have to **confirm** the host you've never establish connection before. Some people will mistaken this and lower the level of the security of his `ssh`(however,  sometimes, lower the level may be a better choice, it depends on the situation you meet with).

What's more, what will happen if I rewrite the RaspberryPi's OS, I mean, using windows terminal without convenient PuTTY tool, how to   [SSH remote host identification has changed](https://stackoverflow.com/questions/20840012/ssh-remote-host-identification-has-changed) . This questions in stacksoverflow solves my problem with this command:

```shell
$ ssh-keygen -R <host>
```

With this command, it will removes all keys belonging to host from known_hosts file.