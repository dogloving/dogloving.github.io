---
layout: post
title: Javascript�еıհ�
date: 2017-2-13
categories: blog
tags: [Javascript,ѧϰ�ʼ�]
---


������˼��һ�����⣺���ͳ��һ�����������˼��Σ�
�����뵽����һ��ȫ�ֱ�����ÿ�������������һ�ξͽ�����++��
```
var count = 0;
function foo(){
    count++;
    alert(count);
}
```
��ô��û�����������أ��հ������Ľ����������⣺
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
�����˽�ʲô�Ǳհ���

> �հ����ɺ�����������ص����û�����϶��ɵ�ʵ�塣(ժ��ά���ٿ�)

�����ó����ܹ���ȡ��Ӧ�����ص����������ڲ��ı����⣬���ܽ���Щ����ʼ�ձ������ڴ��С�
��ô����Ҳ���Կ����հ���һ��ȱ������ڴ����Ĵ����Բ�Ҫ���ñհ���
����Ҳ����������⣺�հ����ں����ڲ�����ġ����ǽ��丸��������һ�����󣬸������ж���ı������������˽�г�Ա����ô�հ������Ƕ���Ĺ��з������Ǳ�¶�����Ľӿڡ�

����������˼���⣬˼�����ǵ����н����
P1:
```
var name = "The Window";
����var object = {
��������name : "My Object",
��������getNameFunc : function(){
������������return function(){
����������������return this.name;
������������};
��������}
����};
����alert(object.getNameFunc()());
```
P2��
```
��var name = "The Window";
����var object = {
��������name : "My Object",
��������getNameFunc : function(){
������������var that = this;
������������return function(){
����������������return that.name;
������������};
��������}
����};
����alert(object.getNameFunc()());
```

�����𰸣�  P1: The Window    P2: My Object
ע��<b>this��ָ�����������ں������õ������ľ����ģ��������������ں�������������ľ����ġ�</b>
���Ե�һ��thisָ����window,�ڶ���this ָ����object��
������ǽ�P1�еĴ���ĳ�
```
var name = "The Window";
����var object = {
��������name : "My Object",
��������getNameFunc : function(){
������������//var that = this;
������������return function(){
����������������return this.name;
������������};
��������}
����};
(function test(){
	name = "test";
	alert(object.getNameFunc()());
})();
```
��ô�������Ľ����  test��


˼����Plus��
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
���Ž������ console.log(item + ' ' + list[i])  �ĳ�  console.log(i)���ܿ��������ˡ�
[��չ�Ķ�](http://stackoverflow.com/questions/111102/how-do-javascript-closures-work)



