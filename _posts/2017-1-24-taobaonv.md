---
layout: post
title: 用python爬取美女照片并分类
date: 2017-1-23
categories: blog
tags: [python,爬虫]
description: 懂得如何科学上网是成为一名优秀程序员的必备技能之一
---

# 乘客们请系好安全带，老司机要发车了
```
#coding=utf-8
#抓取淘宝淘女郎的照片并且对不同人进行分类
import urllib2
import re
import os
from time import sleep
from sys import exit
import random

if not os.path.exists('taobaonv'):
    os.mkdir('taobaonv')
os.chdir(os.path.join(os.getcwd(),'taobaonv'))
path=os.getcwd()


url_base='https://mm.taobao.com/json/request_top_list.htm?page='
global count
global images
dirList=[1]

#匹配出图片网址、照片主名字、照片主地址
pattern=r'<div class="list-item">.*?<img src="(.*?)".*?>.*?<a class=.*?"_blank">(.*?)</a>.*?<span>(.*?)</span>'
header={'User-Agent':'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36'}
#获取该网页信息
def getData():
    #print 'getData start'
    url=url_base+str(count)
    request=urllib2.Request(url,headers=header)
    response=urllib2.urlopen(request)
    global pageData
    pageData=response.read()
    #print 'getData end'
    #print len(pageData)
#存储照片
def saveImage(imageInfor):
    #print 'saveImage start'
    u='http:'+imageInfor[0]
    imageInfo=(u,imageInfor[1],imageInfor[2])
    imageData=urllib2.urlopen(imageInfo[0]).read()
    #当不存在该地区文件夹时
    if imageInfo[2] not in os.listdir(path):
        os.mkdir(imageInfo[2])
        #dirList.append(imageInfo[2])
    path1=os.path.join(path,imageInfo[2])+'\\'
    temp=path1+imageInfo[1]+'.jpg'
    #print a
    f=open(temp,'wb')
    f.write(imageData)
    f.close()
    #print 'saveImage end'
#根据正则表达式匹配出当前页面的所有淘女郎的信息
def getImages():
    #print 'getImages start'
    images=re.findall(pattern,pageData,re.S)
    for i in images:
        saveImage(i)
    #print 'getImages end'

#抓取所有图片
count=3937
while count<=4320:
    print count
    try:
        getData()#获取当前页面的所有信息
        getImages()#获取图片信息并且将他们存到对应位置
    except Exception,ex:  
        print Exception,":",ex
    count+=1
    #t=random.uniform(1,2)
    #print 'rand time: ',t
    #sleep(t)

```















