---
layout: post
title: fq简单教程
date: 2016-12-20
categories: blog
tags: [教程,科学上网]
---

# fq教程


最近在github上看到一个fq工具，觉得非常好用，就在这里分享下。
首先下载地址[点击这里下载](https://github.com/guoruibiao/crosswall/raw/master/res/crowall.rar)。这里我要说下这个程序原理了,下面是程序源代码：
```
# coding:utf-8
import sys

reload(sys)
sys.setdefaultencoding('utf8')
#    __author__ = '郭 璞'
#    __date__ = '2016/10/24'
#    __Desc__ = 翻墙助手， 默认会先备份一下当前的hosts文件，防止出现意外，另外可以跨平台使用

import platform
import os
import urllib2

def downloadHosts(url):
    file = open('./hosts.txt', 'wb')
    data = urllib2.urlopen(url).readlines()
    file.writelines(data)
    file.close()



def crosswall(systemtype='Window'):
    try:
        if systemtype == 'Windows':
            os.system('copy %SystemRoot%\System32\drivers\etc\hosts  %SystemRoot%\System32\drivers\etc\hosts_bak')
            os.system('copy hosts.txt %SystemRoot%\System32\drivers\etc\hosts')
            os.system('ipconfig /flushdns')
            os.system('pause')
            print 'It\'s done on Windows! And Try your browser!'
        elif systemtype == "Linux":
            os.system('cp /etc/hosts /etc/hosts_bak')
            os.system('mv ./hosts.txt /etc/hosts')
            os.system('pause')
            os.system('sudo /etc/init.d/networking restart ')
            print 'It\'s done on Linux! And Try your browser!'
    except Exception as e:
        print e



if __name__ == '__main__':

    url = 'https://raw.githubusercontent.com/racaljk/hosts/master/hosts'
    downloadHosts(url=url)
    print 'Hosts update success!'
    crosswall(platform.system())
    print 'Hosts replaced success! Try to cross the wall!'
```
它首先从https://raw.githubusercontent.com/racaljk/hosts/master/hosts上下载最新的host（这个文件由另一个github进行维护，所以你也可以直接手动将里面的内容拷贝进hosts文件），然后检查你操作系统类型，根据你操作系统类型进行不同操作。我的是windows操作系统，它先将原hosts文件进行拷贝放在原目录下，然后将刚才下载下来的内容拷贝到hosts文件中去，再刷新dns即可。这里要注意我们如果直接对hosts文件进行修改的话会被拒绝，所以我们要用管理员的身份进行操作，即我们先对压缩包进行解压，然后右键crowall.exe以管理员身份运行。
这是一种比较方便的通过修改hosts文件的fq方法，就我目前知道的其他方法还有软件fq（lantern、自由门等等）、VPN之类的，不过后两者每次要使用的话每次都得先手动开启，稳定的VPN还要去网上买，所以感觉修改hosts是我当前认为最经济简单的方法了。
有空再写下fq原理。

