---
layout: post
title:  跨浏览器处理js事件
date:   2016/9/4 11:12:47  
categories: Javascript
tag: 事件
---

* content
{:toc}


- 第一个要创建的方法是`addHandler()`，他的职责是视情况分别使用DOM0级方法、DOM2级方法或IE方法来添加事件。这个方法属于一个名为EventUtil的对象。`addHandler()`方法接受3个参数：要操作的元素、事件名称和事件处理程序函数。

- 与`addHandler()`对应的方法是`removeHandler()`，它也接受相同的参数。这个方法的职责是移除之前添加的事件处理程序，无论该事件处理程序是采取什么方式添加到元素中的，如果其他方法无效，默认采用DOM0级方法。

	    var EventUtil = {
    		addHandler: function(element, type, handler){
    			if (element.addEventLlistener){//优先监测是否存在DOM2级方法
    				element.addEventLlistener(type, handler, false);
    			}else if (element.attachEvent){//其次是IE方法，必须加"on"前缀以兼容IE8和更早的版本
    				element.attachEvent("on"+type, handler);
    			}else {//最后是DOM0方法
    				element["on"+type] = handler;
    			}
    		},
    		removeHandler: function(element, type, handler){//同上
    			if (element.removeEventListener){
    				element.removeEventListener(type, handler, false);
    			}else if (element.detachEvent){
    				element.detachEvent("on"+type, handler);
    			}else {
    				element["on"+type] = null;
    			}
    		}
    	}


- 调用实例


	    var btn = document.getElementById("myBtn");
	    var handler = function(){
	    	alert("Clicked");
	    }
	    EventUtil.addHandler(btn, "click", handler);
	    //省略部分代码
	    EventUtil.removeHandler(btn, "click", handler)
	    //省略部分代码
