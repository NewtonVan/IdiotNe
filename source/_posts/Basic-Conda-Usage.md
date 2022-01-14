---
title: Basic Conda Usage
mathjax: true
date: 2020-07-27 15:15:55
tags: Tools
categories: Programming
---

# Preface
***

Long time no see. This bolg is written for record the knowledge I've learnt during installing pytorch on windows. And I'll introduce some basic knowledge about virtual environment, update and etc. Attention that these command or method is suit for windows, most of them will be suit for linux.

# Check the pagkage's location
***

It's really import for me to confirm where the file/program consume the space of my disk. To check the python module package's path. You can try this:

```python
import module
print(module.__file__)
```

In general, ananconda's package will be installed follow this path `[your anaconda's directory]\Lib\site-packages`

# Virtual Environment
***

Creating virtual environment aim to better run other's python program which may have difference among their version. What's more, programming in a virtual environment will prevent the conflict among the global python module. 

## Create
***

```shell
conda create -n my_env_name python=3.6
```

On windows, run this command on cmd, and you will create a new virtual environment with the name you replace at my_env_name.

## Check your virtual environment
***

Check your virtual environment's list in this way:

```shell
conda info --envs
```
or this way

```shell
conda env list
```

## Activate your Virtual Environment
***

```shell
conda activate my_env_name
```

This command will help you enter into the correspond virtual environment. Normally, your terminal will look like this:

```shell
(my_env_name)[user_name](blablabal..)
```

## Quit the Current Virtual Environment
***

```shell
conda deactivate
```

Some blogs resquire your env_name after the *deactivate*, however I've find some error about this method. And I find this solution from an github issue. It suits my condition well.

## Install Package At The Specific Virtual Environment
***

One of the virtual environment's advantages is that you can install your package without considering the potential conflict among the global package. You can install your package, and its effect domain will be constrained into the specific virtual environment. 


```shell
conda install -n my_env_name [package]
```

or you can activate the specific virtual environment and use `pip install` at current virtual environment.


## Remove the Virtual Environment
***

```shell
conda remove -n my_env_name --all
```

This command will remove my_env_name virtual environment.


## Remove the Package In the Virtual Environment
***

```shell
conda remove -n my_env_name package
```

**warning: still unsure this command**

## Handle the global package
***

Check the installed global package:
```shell
conda list
```

Install global package:
```shell
conda install package
```

## Configure yml file to create a new environment
***

Example yml file:

```yml
name: my_env_name
dependencies:
- python=3.6
- pytest
- keras
- tqdm
- Pillow
- pip:
    - tensorflow
```

Warning: I'm not quite sure about this method.

Then you can create a new virtual environment by this command:

```shell
conda env create -f env_config.yml
```



## Share Your Environment

***

### Export your Environment yml file

***



```
conda env export > [environment yml file name].yml
```



### Clone your Environment

***

```
conda create -n [new environment name] --clone [existed environment name]
```

 

## What's more

***

 For the command that you are not familiar with, you can check it's usage by add a ``-h`` at the end of the command.



## Some blogs

[conda  usage]([http://course.killf.info/content/00-14%E6%95%B0%E6%8D%AE%E5%88%86%E6%9E%90/md/shuju-conda.html#huanjing](http://course.killf.info/content/00-14数据分析/md/shuju-conda.html#huanjing))