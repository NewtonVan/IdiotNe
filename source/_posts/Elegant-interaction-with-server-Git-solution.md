---
title: 'Elegant interaction with server: Git solution'
mathjax: true
date: 2022-01-15 13:20:13
tags:
categories: Tricks
---

# Background

***

## Common Development Paradigms

***

* local: development
* remote: running

## Tools

***

* Git
* `Vscode` with extensions for remote development
* ssh
* docker



# Object

***

## local

***

* Convenience with IDE
  * bad case: development only with shell
* Local side and remote side build up well-organized version control

## Remote

***

* Convenient version control
  * after push from local side, remote side will automatically sync with pushed branch.
* Create virtual environment
  * Well isolated
  * Portable
  * Friendly rebuild



# Plan

***

## Git 

***

### Remote

***

* Build up `repo` .

```shell
git --bare init [仓库名].git
```

* Configure authority.

```shell
git config receive.denyCurrentBranch ignore
```

* Record current directory path.
* Enter into `hooks` directory.

```Bash
cd hooks  
vim post-receive 
```

* File `post-receive` help us sync our code.
* File content, `git-dir` usually will be ignored.

```Bash
#!/bin/sh
git --work-tree=[Which directory to sync server-side code to] --git-dir=[Server-side repository address] checkout -f
```

* Explanation for `post-receive` .

[使用git在服务器上部署git仓库并实现提交代码时同步代码到生产环境 - 服务器运维 – 宋巧林的博客](http://www.songqiaolin.com/index/resource/view/id/5.html)

* Remember add `x` flag for file.

### Local

***

* Most important information for local side is address for remote `repo` : `ssh://[user@ip]:[``server`` file path]` 

[用git在服务器部署你的代码、同步文件](https://www.jianshu.com/p/821ff301cbed)



# Reference

***

- [使用git在服务器上部署git仓库并实现提交代码时同步代码到生产环境 - 服务器运维 – 宋巧林的博客](http://www.songqiaolin.com/index/resource/view/id/5.html)
- [Aurora-龙振巅峰的博客](https://auroralzdf.github.io/2017/09/23/线上服务器搭建GIT服务器，实现本地代码上传并同步到服务器/)
- [搭建自己的Git服务器，实现团队协作](https://cidoliu.github.io/2020/12/01/NewGitServer/)
- [用git在服务器部署你的代码、同步文件](https://www.jianshu.com/p/821ff301cbed)
