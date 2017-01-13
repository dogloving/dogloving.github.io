---
layout: post
title: 如何使用github pages搭建个人博客
date: 2016-12-21
categories: blog
tags: [教程,网站]
---

> 好好学习，天天向上
之前有买过godaddy的虚拟主机，一个月47块钱，然而就一开始玩了几天，后来就没动过了。昨天偶然在github右上角发现用github pages搭建个人主页的消息，如发现新大陆。花了一天时间做了个自己的网站。
前期准备：有一个github的账号（如果没有去申请一个，免费的）；本地安装git（具体可参考[廖雪峰的git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)）
第一步：新建一个仓库，命名为*yourname.github.io*；
第二步：将代码clone到本地，然后本地新建文件，然后push到github上；这里我推荐使用jekyll框架，能够节省不少时间，下面是我今天刚看到的[用Jekyll搭建博客](https://zryfish.github.io/jekyll/others/2015/05/18/jekyll-how-to/)。我本人是直接fork了github上另一个用户的[模板](https://github.com/cnfeat/blog.io)，我记得在新建 yourname.github.io仓库时会提示是否将已有仓库中的文件导入到新仓库中；然后将里面的内容修改为自己的即可。这时候，你在浏览器地址栏中输入*yourname.github.io*就能进入你的个人主页啦。
第三步：如果你不喜欢这个域名，那么你可以自己购买域名，然后添加域名的dns解析，具体可以参考下面这篇博客[GitHub Pages 绑定来自阿里云的域名](http://quantumman.me/blog/setting-up-a-domain-with-gitHub-pages.html)

完成以上三步，就能拥有一个自己的博客了。不过使用github pages 搭建博客既有好处也有坏处。好处是它是免费的，好像是能有300M的免费空间给你使用；坏处就是你网站中有什么东西别人都能一目了然，同时也可能被fork，没有试过private repository，因为穷。

