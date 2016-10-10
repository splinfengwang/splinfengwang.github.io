---
layout: post
title:  this指向target和currentTarget
date:   2016/9/5 12:32:47  
categories: Javascript
tag: 事件
---

* content
{:toc}


属性/方法 | 类型 | 说明
---|---|---
currentTarget | Element | 其事件处理程序当前正在处理事件的那个元素
target | Element | 事件的目标



    var btn = document.getElementById("myBtn");
    btn.onclick = function(event){
    	alert(event.currentTarget === this); //true
    	alert(event.target === this); //true
    }


这个例子检测了currentTarget和target与this的值。由于click事件的目标是按钮，因此这三个值是相等的。如果事件处理程序存在于按钮的父节点中（例如document.body），那么这些值是不同的。再看下面的例子。


    document.body.onclick = function(event){
    	alert(event.currentTarget === document.body); //true
    	alert(this === document.body); //true
    	alert(event.target === document.getElementById("myBtn")); //true
    }


单击这个例子中的按钮时，this和currentTarget都等于document.body，因为事件处理程序是注册到这个元素上的。然而，target元素却等于按钮元素，因为它是click事件真正的目标。由于按钮上并没有注册事件处理程序，结果click事件就冒泡到document.body，在那里事件才得到了处理。