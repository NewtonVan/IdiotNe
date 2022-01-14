---
title: Building your own blog!
date: 2019-07-31 13:14:25
tags: 
	- Blog
	- Front-end
categories: Misc
---

# Overview
***
## Git
* Download **git**, after that use bash to operate.
* Set the configuration (I will show how to set the configuration on my another blog)
* Create a new file to store your blog. 
* Then open **git bash** at this file.
* Then we need to set SSH key

### SSH key
* Enter this command `ssh-keygen -t rsa -C "Your mail address"`. 
* Then you will see Git ask you to "Enter file in which to save the key", just press Enter.
* Then you will be asked to Enter a code, it is linux style, which means that you can't see the code you type. 
![Enter your Passphrase](https://pic4.zhimg.com/80/v2-2cb74afa9b7c9077b33da54d4513523b_hd.jpg)
* When you see this, it means your ssh key is successfully set.
![Eureka](http://img.voycn.com/images/2019/05/c0a0f40a943fd5126ff4b6706b9922ee.png)
* Find `.ssh\id_rsa.pub` (its path is showed in the introduction after you successfully set the ssh key)
* Use **Nodepad++** (because of stupid microsoft) to open this file and copy its contents.
* Open your *Github*, click your *picture*, then click *settings*, and click
* **SSH and GPG keys**, choose **New sskey**
![Set ssh key on your gitbub](http://img.voycn.com/images/2019/05/28f50b516fc60b575b8318d0d3c8db51.png)
* Test this by `ssh -T git@github.com`
* Then use these two commands

>`git config --global user.name "your id"`  
>`git config --global user.email "your email bond with your github"`



# Install Node.js
***
I will show how to install this on another blog.

# Hexo
***
* Open *gitbash* at the place where you are going to set your blog.
* Enter `npm install hexo-cli -g`
* Then enter `hexo -v` to test whether Hexo is successfully installed.
![Install Hexo](http://img.voycn.com/images/2019/05/4fca51e6b5457f5cd09efddf36843467.png)
* Enter `npm install hexo --save`
* To confirm the current document file is empty.
* Run the command `hexo init`
* You can see this in your document file

![](http://img.voycn.com/images/2019/05/89bb9e3a1f43a939055a72eabe76dbec.png)

# Begin to build up your blog
***
![How to set your blog](http://img.voycn.com/images/2019/05/f61b966754e4d38bc7e10cc19d653682.png)

* connect Hexo and your gitbub

![Link Hexo and githbu](http://img.voycn.com/images/2019/05/e416f23faabb4711ef25fcaf40c4b59b.png)

* Then use *gitbash* 
>`hexo g`
>`hexo s`
>`npm install hexo-deployer-git --save`
>`hexo d`

* Then you can see your blog by this site `https://yourid.github.io`