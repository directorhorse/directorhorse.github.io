---
layout: post
title: "github与gitee合作以在githubpage显示图片"
date:   2024-5-10
tags: [博客]
comments: false
author: directorhorse
---
&emsp;&emsp;一般来说，在使用githubpage制作博客的时候引用图片，使用的是github里图片的网络地址。但由于众所周知的原因，github在国内访问时断时续，经常加载不出来图片。这个问题可以使用图床来解决，但是图床也是需要服务器的，要么租服务器，要么用对象存储服务，总之都得花钱。 \
&emsp;&emsp;换个思路，github不容易访问，但gitee是访问很快的。我们可以把项目挂载到gitee上，在github里用gitee的地址，这不就解决了吗。
## 1.在gitee上同步github项目
&emsp;&emsp;gitee新建仓库可以选择url，从github克隆项目，如图所示。\
<img src="https://gitee.com/directorhorse/directorhorse.github.io/raw/main/images/2024-5-10-githubpage博客/导入仓库.png" alt="示例图片" width="100%" />
&emsp;&emsp;导入仓库后，需要找到图片的地址。这是十分容易的，我们在项目里找到一个图片并打开，会看到网址，以https://gitee.com/directorhorse/directorhorse.github.io/blob/main/images/404.jpg为例，把blob换成raw，得到的就是图片的网络地址https://gitee.com/directorhorse/directorhorse.github.io/raw/main/images/404.jpg。下面这张图就是引用的网络图片 \
<img src="https://gitee.com/directorhorse/directorhorse.github.io/raw/main/images/404.jpg" alt="示例图片" width="50%">

## 2.git同时推送到两个仓库
&emsp;&emsp;git可以设置多个推送地址，使用以下命令进行设置地址与推送
```
//添加一个新仓库
git remote add origin2 xxxxxxx
//新仓库拉取
git pull origin2
//推送
git push origin
git push origin2
```
## 3.设置head头
&emsp;&emsp;做完以上工作我们发现图片加载不出来了，这是因为http请求会携带一个referrer头，记录发起请求的源地址，gitee的服务端应该是不允许来自非本身的地址请求图片资源。所以要想办法去掉referrer。
&emsp;&emsp;本博客使用到了模板，因此可以在模板html添加如下代码
```
<head>
<meta name="referrer" content="no-referrer">
</head>
```