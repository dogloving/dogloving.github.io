---
layout: post
title: WSL---在Windows下也能使用Linux
date: 2017-07-22
categories: blog
tags: [教程]	
---

​	今天发现了一个很好玩的东西------*WSL(Windows Subsystem Linux)*，是个能在不安装双系统和虚拟机的情况下使用*Linux*的东西。废话少说，直接上图：

![](https://raw.githubusercontent.com/dogloving/dogloving.github.io/master/img/20170722/bash.png)

​	从图中可以看出当前系统是*Windows*，*bash*中的是*Linux*系统。下面是安装*WSL*的方法：

###  安装步骤

首先系统必须是*Win10*，而且版本需要在1607以上(我的是1703). 关于如何查看自己电脑系统的版本：*设置--系统--关于*，就能看到自己的*Windows*版本了。如果系统很久没更新了，我推荐使用*Windows*官网的系统升级软件[易升](http://go.microsoft.com/fwlink/?LinkId=691209)。

![](https://pic1.zhimg.com/v2-830b95686cde605084b110cfe7cfbaf8_b.png)

然后需要开启开发者模式，这个在 *设置--更新和安全--针对开发人员*中。

![](https://pic1.zhimg.com/v2-2b2e6439e33068c37037e04fe72de444_b.png)

接着开启*Windows*功能中的*WSL*，这个在 控制面板--程序--打开或关闭*Windows*功能。

![](https://pic4.zhimg.com/v2-57772276bd30e0872687a9dfbac3a6a7_b.png)

搞好这些东西之后就可以开始安装*Ubuntu*了。打开*powershell*，输入*bash*，然后输入*y*确定安装即可。

![](https://pic1.zhimg.com/v2-c9731d9d7222b8812d73aa64233089f0_b.png)



之后就是设置用户名和密码了。我这里推荐使用英文的用户名。然后就可以愉快的体验*Linux*了。

*Windows*是挂载在*/mnt*下的，所以在*bash*中可以访问*Windows*中的文件(除了部分需要一定权限的目录或文件)。

关于更多功能请参考[简明的WSL教程](https://zhuanlan.zhihu.com/p/24537874)。上面内容参考了该文章，且使用部分图片。

### 界面美观

*Windows*下无论是*powershell*还是*cmd都*很丑，下面我介绍一下我自己的配置方法。

首先更换字体，我从[这里](https://be5invis.github.io/Iosevka/inziu.html)下载了知乎*B*大设计的字体(个人觉得还不错)，然后将这些字体加入到*控制面板--外观和个性化--字体*(就是把字体文件直接拖动到里面)。之后在*powershell*上右键设置。这个比较简单就不写了。*Ubuntu**的背景色是*RGB(40,0,30)。

