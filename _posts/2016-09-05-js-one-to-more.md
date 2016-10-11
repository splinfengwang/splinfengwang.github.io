---
layout: post
title:  通过一个函数处理多个事件
date:   2016/9/5 14:52:47  
categories: Javascript
tag: 事件
---

* content
{:toc}


event.type搭配switch语法

    var btn = document.getElementById("myBtn");
    var handler = function(event){
	    switch(event.type){
		    case "click" :
			    alert("click");
			    break;
		    case "mouseover" :
			    alert("mouseover");
			    break;
		    case "mouseout"
			    alert("mouseout");
			    break;
	    }
    }
    btn.onclick = handler;
    btn.onmouseover = handler;
    btn.onmouseout = handler;


附一个别人的文章讲的比较详细：[《我也来说说js的事件机制》](http://www.w3cfuns.com/notes/17398/8062de2558ef495ce6cb7679f940ae5c.html)
