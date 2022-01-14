---
title: virtual machine
mathjax: true
date: 2019-09-23 22:23:50
tags: CTF
categories: Programming
---

# Overview
***

"When you say, "I wrote a program that crashed windows", people just stare at you blankly and say, "hey, I got those with the system, for free""  By **Linus**

Fxxk you windows!!!

When windows updates, the world goes to crazy. And I have to reunistall the virtual machine to install linux.

# Download Vmware
***

Remember that, always use the register code you can find in the internet rather than the software that has been hacked.


# Create The Machine
***

There are several tips that needed to be attentioned. You'd better devide your space of the disk by your hand. 

Always remember that, the default settings always have trouble, so you'd better handle it yourself.


| Region | Space | Sort | Type |
|---|---|---|---|
| /. | 25%-35% space | Main | ext4 |
| /boot | 200M | Main| ext4 |
| /home |   remain space  | Logical | ext4 |
| /swap |  6G    | Logical | swap space |

# Set The Settings
***

Click edit your settings. 

The processor choose 4.

CD/DVD SATA choose the iso you download.

The Internet choose the NAT.

# Install VM-Tools
***

Click the "virtual machine" button on the side bar. Install the VM-Tools and restart your linux. 


# Make It Accept 32-bit program
***

Unlike windows, it will not accept 32-bit program if it is a 64-bit linux. Maybe this is the only advantage of windows.

Just implement these commands in terminal.

```
sudo apt-get update 
sudo apt-get install libc6:i386 -y
sudo apt-get install lib32ncurses5 lib32z1 -y
sudo apt-get install  gcc-multilib -y
```

Everything is OJBK.

# IDA Dynamic Debug
***

[TUTORIAL](https://bbs.pediy.com/thread-247830-1.html)

# Install qemu To Fit MIPS
***

`sudo apt-get install qemu`

To run the big port use command:
`qemu-mips <file name>`

Run the small port:
`qemu-mipsel <file name>`

# Clean Your boot
***

After your linux kernel has been updated, your space for /boot may be narrow. Here are the blogs which introduce the method to clean your space.

[Linux](https://www.linuxidc.com/Linux/2017-12/149655.htm)

[cnblogs](https://www.cnblogs.com/carle-09/p/11363020.html)

[COSCHINA](https://my.oschina.net/u/931493/blog/512227)