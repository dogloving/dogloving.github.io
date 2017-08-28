---
layout: post
comments: true
title: 安装linux双系统并配置开发环境
date: 2017-1-31
categories: blog
tags: [记录]
---

因为社团项目在windows下开发不是很方便，所以决定搭建个linux环境。

# 一：搭建windows-linux双系统

* 压缩磁盘  右键计算机/我的电脑-管理-磁盘管理，选择一个磁盘并设置压缩大小进行压缩；
* 下载镜像文件并制作启动盘 具体步骤可见[deepin官网教程](https://www.deepin.org/installation/)。大概就是先下载对应的镜像文件（32位/64位），然后进入镜像文件双击一个***_b.exe的文件，选择刚才的镜像文件开始制作启动盘
* 重启电脑，进入BIOS界面（华硕笔记本是f2），选择BOOT，将刚才的镜像文件设置为第一启动项，然后自己设置下一些信息

# 二：安装配置开发环境

* 首先配置php+Apache+mysql环境。去[XAMPP官网](https://www.apachefriends.org/zh_cn/download.html)下载对应版本的安装包，然后在下载目录下打开命令行，输入 ```sudo ./[文件名]```，然后程序就默认安装在/opt/lampp下了。这时候在浏览器中输入```http://localhost```应该会有东西出现，表示安装成功。
* 然后安装git。先升级apt-get（```sudo apt-get update```）,之后终端中输入```sudo apt-get install git```,然后进行配置。书短重输入```ssh-keygen -t rsa -C "your email"```，三次回车，再输入```cd ~/.ssh```进入.ssh目录（貌似这个文件夹是隐藏的），打开id_rsa.pub，拷贝里面的内容（```nl id_rsa.pub```）。浏览器上打开登录github，进入settings-SSH and GPG keys-New SSH key，将复制的内容粘贴进去。注意要以ssh-rsa开头，如果没有请加上。
* 安装运行docker和docker-compose。（可参见学长给的[教程](http://www.jianshu.com/p/0b3d8d264414)）输入```sudo service docker start```启动docker，然后进入10WEB目录（git clone到/opt/lampp/htdocs目录下），里面有一个docker-compose.yml文件。终端下输入```sudo service docker-compose up```启动前台。第一次会下载一些东西比较慢，后面好了。然后打开http://localhost:6070就进入亿灵首页了，输入http://localhost:8081就是数据库了。
