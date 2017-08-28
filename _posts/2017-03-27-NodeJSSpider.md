---
layout: post
comments: true
title: NodeJS爬虫
date: 2017-03-27
categories: blog
tags: [记录]
---

因为D类课大作业需要用到NodeJS爬虫的缘故，所以学了一下怎么用NodeJS爬虫，虽然用着没有Python爽，但是也还不错。今天试着用NodeJS爬了社区评论，发现并没有相像中的那么简单。下面通过代码来回顾一下几个坑点吧：

```
//获取文章下第一个评论的作者和其评论内容
var superagent = require('superagent');
var cheerio = require('cheerio');
var url = require('url');
var eventproxy = require('eventproxy');
var fs = require('fs');


var url1 = 'https://cnodejs.org';
var header = {
	"Accept":"text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8",
	"Accept-Encoding":"gzip, deflate, sdch, br",
	"Accept-Language":"en-US,en;q=0.8,zh-CN;q=0.6,zh;q=0.4,zh-TW;q=0.2",
	"Cache-Control":"no-cache",
	"Connection":"keep-alive",
	"Cookie":"UM_distinctid=15af649065e105-008cd6c1217ddb-5e4f2b18-144000-15af649065f174; connect.sid=s%3ATq8x2T0fHAw9GEEpPVtm-hoSuK401_16.18Jmgtn9ao9WSf4xaxUQsPZpfonOdmsY70MXDTy4v9w; _ga=GA1.2.1607436373.1490190665; _gat=1; CNZZDATA1254020586=756749598-1490189541-https%253A%252F%252Fwww.google.com%252F%7C1490608590",
	"Host":"cnodejs.org",
	"Pragma":"no-cache",
	"Upgrade-Insecure-Requests":"1",
	"User-Agent":"Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/56.0.2924.87 Safari/537.36"
};
superagent.get(url1).end(function(err,res){
	if(!err && res.statusCode == 200){
		var $ = cheerio.load(res.text);
		var urlList = [];
		var zero = [];
		var list = $('.topic_title');
		var zeroList = $('.unstyled').children();
		zeroList.each(function(index,element){
			var $$ = cheerio.load(element);
			var href = $$('a').attr('href');
			zero.push(url1+href);
		});
		list.each(function(index,element){
			var $element = $(element);
			var tmp = url1+$element.attr('href');
			if(zero.indexOf(tmp) == -1){
				urlList.push(tmp);
			}
		});
		console.log(urlList.length);
		var ep = new eventproxy();
		ep.after('my_html',urlList.length,function(contents){
			console.log('fuck');
			contents = contents.map(function(pair){
				var user = pair[0];
				var comment = pair[1];
				return ({
					'user': user,
					'comment': comment
				});
			});
			fs.writeFileSync('fuck.json',JSON.stringify(contents));
			console.log('ok');
		});

		var count = 100;
		urlList.forEach(function(url){
			setTimeout(function(){
				superagent.get(url).set(headers=header).send().end(function(err,res){
				if(!err && res.statusCode == 200){
					var $ = cheerio.load(res.text);
					var user = $('.reply_author').first().text();
					var comment = $('.markdown-text').eq(1).text();
					ep.emit('my_html',[user,comment]);
				}else{
					console.error(err);
				}
			});
			},count);
			count  = count + 100;
		});
	}
});
​```
```

##  坑点一：NodeJS的异步

NodeJS的一大优势就是异步，但是在爬虫的时候异步可能就会带来麻烦，比如我们在某首页爬取到40个链接，然后又在循环中去爬这40个链接中的内容。但是因为是异步执行的，所以就算循环中还没结束，外部结束了，整个爬虫过程就结束了。解决方法一般是两个：1.使用回调函数；2.使用计数器，而为了方便用户，NodeJS提供了一个叫eventproxy的轻量级模块，其作用类似于一个高级计数器，具体用法见[链接](https://github.com/alsotang/node-lessons/tree/master/lesson4)。



##  坑点二： 访问过快返回503错误

用于Javascript中没有sleep函数，所以这里我用了setTimeout



##  坑点三： request和superagent返回信息不同

因为返回的是gzip格式，request需要手动ungzip，而superagent会帮你自动ungzip





#  相对于Python的好处：快！！！

因为Javascript本身就是干这事的，所以在解析字符串这方面自然快啦，而且cheerio用法和JQuery类似，个人觉得比BeautifulSoup好用些。最后附上Python版本的代码：

```
#coding=utf-8
import requests
import json
from bs4 import BeautifulSoup

url = 'https://cnodejs.org'

r = requests.get(url)

soup = BeautifulSoup(r.text,'lxml')
aList = soup.find_all('a',class_='topic_title')
urlList = []
for i in aList:
	urlList.append(url+i['href'])
bList = soup.find_all('span',class_='count_of_replies')
#由于部分文章是没有评论的，所以我们将这些没有评论的url记录下来，到时候不去爬取他们就行了
zeroList = []
num = list(soup.find('ul',class_='unstyled').children)
count = 0
for i in bList:
	if(i.text.strip() == '0'):
		zeroList.append(urlList[count+num])
	count += 1

result = []
for url2 in urlList:
	print(url2)
	if url2 in zeroList:
		continue
	r2 = requests.get(url2)
	soup2 = BeautifulSoup(r2.text,'lxml')
	user = soup2.find('a',class_='dark reply_author').text
	comment = soup2.find_all('div',class_='markdown-text')[1].find('p').text
	result.append({'user':user,'comment':comment})

print(result)
js = json.dumps(result,ensure_ascii=False)
print(js)
with open('fuck2.json','w') as f:
	json.dump(js,f)
```

参考网站：

[《使用 superagent 与 cheerio 完成简单爬虫》](https://github.com/alsotang/node-lessons/tree/master/lesson3)

[《使用 eventproxy 控制并发》](https://github.com/alsotang/node-lessons/tree/master/lesson4)

[Beautiful Soup 4.4.0 文档](http://beautifulsoup.readthedocs.io/zh_CN/latest/)

[Request快速上手](http://docs.python-requests.org/zh_CN/latest/user/quickstart.html)

[读写JSON数据](http://python3-cookbook.readthedocs.io/zh_CN/latest/c06/p02_read-write_json_data.html)