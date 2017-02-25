---
layout: post
title: Javascript中的闭包
date: 2017-2-13
categories: blog
tags: [Javascript,学习笔记]
---


首先来思考一个问题：如何统计一个函数调用了几次？
马上想到定义一个全局变量，每当这个函数调用一次就将变量++：
```
var count = 0;
function foo(){
    count++;
    alert(count);
}
```
那么有没有其他方法呢？闭包完美的解决了这个问题：
```
function foo1(){
	var n = 0;
	function foo2(){
		alert(n);
		n += 1;
	}
	return foo2;
}

var x = foo1();
x();
```
首先了解什么是闭包：

> 闭包是由函数和与其相关的引用环境组合而成的实体。(摘自维基百科)

其作用除了能够读取本应被隐藏的其他函数内部的变量外，还能将这些变量始终保存在内存中。
那么我们也可以看出闭包的一个缺点就是内存消耗大，所以不要滥用闭包。
我们也可以这样理解：闭包是在函数内部定义的。我们将其父函数视作一个对象，父函数中定义的变量视作对象的私有成员，那么闭包看作是对象的共有方法，是暴露出来的接口。

下面是两道思考题，思考他们的运行结果：
P1:
```
var name = "The Window";
　　var object = {
　　　　name : "My Object",
　　　　getNameFunc : function(){
　　　　　　return function(){
　　　　　　　　return this.name;
　　　　　　};
　　　　}
　　};
　　alert(object.getNameFunc()());
```
P2：
```
　var name = "The Window";
　　var object = {
　　　　name : "My Object",
　　　　getNameFunc : function(){
　　　　　　var that = this;
　　　　　　return function(){
　　　　　　　　return that.name;
　　　　　　};
　　　　}
　　};
　　alert(object.getNameFunc()());
```

公布答案：  P1: The Window    P2: My Object
注意<b>this的指向是由它所在函数调用的上下文决定的，而不是由它所在函数定义的上下文决定的。</b>
所以第一个this指的是window,第二个this 指的是object。
如果我们将P1中的代码改成
```
var name = "The Window";
　　var object = {
　　　　name : "My Object",
　　　　getNameFunc : function(){
　　　　　　//var that = this;
　　　　　　return function(){
　　　　　　　　return this.name;
　　　　　　};
　　　　}
　　};
(function test(){
	name = "test";
	alert(object.getNameFunc()());
})();
```
那么最后输出的结果是  test。


思考题Plus：
```
function buildList(list) {
    var result = [];
    for (var i = 0; i < list.length; i++) {
        var item = 'item' + i;
        result.push( function() {console.log(item + ' ' + list[i])} );
    }
    return result;
}

function testList() {
    var fnlist = buildList([1,2,3]);
    // Using j only to help prevent confusion -- could use i.
    for (var j = 0; j < fnlist.length; j++) {
        fnlist[j]();
    }
}

 testList() //logs "item2 undefined" 3 times
```
试着将上面的 console.log(item + ' ' + list[i])  改成  console.log(i)就能看出问题了。
[拓展阅读](http://stackoverflow.com/questions/111102/how-do-javascript-closures-work)



