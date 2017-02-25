---
layout: post
title: 安装React-Native
date: 2017-2-25
categories: blog
tags: [记录]
---

主要参考[React-Native官方中文文档](https://reactnative.cn/docs/0.41/getting-started.html#content)。
# 第一步 下载Nodejs和npm
[Nodejs下载地址](https://nodejs.org/download/release/v7.6.0/)
[npm下载地址](https://nodejs.org/dist/npm/)
选择适合自己版本的下载，貌似最新的Nodejs中已经有了npm。如果在用npm安装模块的时候出现错误多半是因为Nodejs版本错误。注意x64的电脑下载64-bit的，x86的电脑下载32-bit的。(https://nodejs.org/en/download/)
如果是分开下载的，把npm文件夹放到C:\Program Files (x86)\nodejs\node_modules下

#第二步 下载安装JDK

现在CMD中输入java -version可以查看有没有安装过JDK。如果没有的话，去[官网](http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html)下载一个1.8版本的。然后将路径添加到环境变量。

#第三步 下载Android SDK和安装Android Studio

[Andriod Studio下载地址](https://developer.android.com/studio/index.html#downloads)
如果下载的Android Studio没有自带SDK，那么下载地址的最下面是纯SDK。
安装Android Studio的时候注意不要在路径中带有中文，这点非常重要。

#第四步  按照官网教材配置Android Studio

略

#第五步 安装React-Native

CMD中输入(最好在管理员身份打开)npm install -g react-native-cli。（话说npm真是个好东西）。

#第六步 尝试运行

首先打开Android Studio模拟器（一定要先开启模拟器并开机）
然后选择一个目录下输入
<code>
react-native init AwesomeProject
cd AwesomeProject
react-native run-android
</code>
如果这时候能够完美运行，那就谢天谢地了。说明人品很好。我当时遇到的一个报错是
```
ENOENT: no such file or directory, open react-native 'C:\TDM-GCC-64\BIN;C:MINGW\BIN;C:User\AppData\Local\Temp'
```
心想这是啥玩意儿啊。去StackOverflow上也没找到答案。但是看这个貌似很熟悉的路径。打开环境变量，发现果然这三个是TEMP变量的路径。删掉这个路径，重新react-native run-android. nice! 完美运行!

#改进

根据官网的提示下载个[genymotion](https://www.genymotion.com/download/)，打开后Add一个合适的版本，这样就连Android Studio也不用开了。 nice!

#总结

讲道理，要完成以上这些步骤最好还是有老司机带着，不然弄个一两天都完不成，碰到问题也不知道该怎么办。相比之下，react.js的安装要容易得多了。