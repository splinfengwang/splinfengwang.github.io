---
layout: post
title:  常用DOM节点操作
date:   2017/03/24 22:10:47  
categories: Javascript
tag:
---

* content
{:toc}

```Javascript
    document.createElementFragment('div');  //创建一个DOM片段
    document.createElement('div');  //创建一个具体元素
    document.createTextNode();  //创建一个文本节点
    el.cloneNode();   //克隆一个节点
    el.appendChild(el); //尾部添加一个节点
    replaceChile(el1, el2); //替换两个节点
    el.insertBefore(el);    //在前面插入节点
    document.getElementById('id');
    document.getElementsByName('name');
    document.getElementsByTagName('tagName');
```
