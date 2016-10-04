---
layout: post
title:  跨浏览器的事件对象处理
date:   2016/9/5 14:52:47  
categories: Javascript
tag: 事件
---

* content
{:toc}


	var EventUtil = {
	    addHandler: function(element, type, handler){
	        if (element.addEventLlistener){//优先监测是否存在DOM2级方法
	            element.addEventLlistener(type, handler, false);
	        }else if (element.attachEvent){//其次是IE方法，必须加"on"前缀以兼容IE8和更早的版本
	            element.attachEvent("on"+type, handler);
	        }else {//最后是DOM0方法-->
	            element["on"+type] = handler;
	        }
	    },
	   
	    getEvent: function(event){
	        return event ? event : window.event;
	    },//区别event是否为IE
	    
	    getTarget: function(event){
	        return event.Target ? event.Target : event.srcElement;
	    },//同上
	    
	    preventDefault: function(event){
	        if(event.preventDefault){
	            event.preventDefault();
	        }else{
	            event.returnValue = false;
	        }
	    }
	    
	    removeHandler: function(element, type, handler){//同上
	        if (element.removeEventListener){
	            element.removeEventListener(type, handler, false);
	        }else if (element.detachEvent){
	            element.detachEvent("on"+type, handler);
	        }else {
	            element["on"+type] = null;
	        }
	    }
	    
	    stopPropagation: function(event){
	        if(event.stopPropagation){
	            event.stopPropagation();
	        }else{
	            event.cancelBubble = true;
	        }
	    }
	}


* 我们为EventUtil添加了四个方法，调用实例，必须有一个事件对象传入到事件处理程序中，而且要把该变量传给这个方法。

	    btn.onclick = function(event){
	    	event = EventUtil.getEvent(event); //拿到这个对象
	    	EventUtil.preventDefault(event); //传递到方法里面去
	    }
    