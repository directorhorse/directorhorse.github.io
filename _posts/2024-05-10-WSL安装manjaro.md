---
layout: post
title: "WSL安装manjaro"
date:   2024-5-10
tags: [linux]
comments: false
author: directorhorse
---
## 关于WSL
&emsp;&emsp;WSL是适用于windows的linux子系统(windows subsystem for linux)。WSL1与WSL2的实现原理不同，WSL1是基于win32api的，相当于把posix接口翻译成win32api，优点是性能高，缺点是兼容性差；WSL2则是基于hyperv，是完整的内核，性能不如WSL1但兼容性很好。\
&emsp;&emsp;为什么用WSL而不是VMware等虚拟机呢？首先，WSL与windows融合的比较好，割裂感很少；其次，WSL可以直接用显卡驱动，VMware则麻烦的多。而且WSL里windows的盘都挂载到了mnt下，不需要像VM那样设置共享文件夹，比较方便。
## 关于manjaro
&emsp;&emsp;manjaro是一个基于archlinux的发行版。与archlinux相比，它降低了安装使用难度，同时能享受丰富的软件库。我之前在Ubuntu安装scala需要从官网下载源码，自己编译，还得手动配环境变量，非常麻烦。而arch软件库本身就有scala，一行pacman或者yay直接搞定。(ps:安装scala是为了使用chisel) \
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;![manjaro](https://gitee.com/directorhorse/directorhorse.github.io/raw/main/images/2024-5-10-wsl安装manjaro/manjaro.jpg)
## 安装过程
### 1.开启WSL
&emsp;&emsp;这一步不再多说，网上教程非常多。
### 2.下载安装社区开发的ManjaroWSL2
&emsp;&emsp;虽然微软官方仅仅为WSL提供了Ubuntu支持，但实际上WSL可以运行任何发行版。微软官方的推荐是在Ubuntu里使用docker运行自己想要的系统，然后打包docker，再用WSL导入。
&emsp;&emsp;本文采用了社区开发的[一键安装工具](https://github.com/sileshn/ManjaroWSL2/releases/tag/20240501)，打开后可发现有一个可执行文件，运行可执行文件，在弹出的终端中添加新用户即可。\
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;![解压后](https://gitee.com/directorhorse/directorhorse.github.io/raw/main/images/2024-5-10-wsl安装manjaro/解压后文件.png)
### 3.进入终端
&emsp;&emsp;如果你此前已有Ubuntu，那么直接运行WSL进入的是Ubuntu而不是manjaro。在windows终端里运行wsl -d manjaro，直接进入manjaro