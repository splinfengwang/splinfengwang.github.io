---
layout: post
title:  eventPhase属性确定事件流阶段
date:   2016/9/8 14:52:47  
categories: Javascript
tag: 事件
---

* content
{:toc}


* 捕获阶段，eventPhase=1；
* 事件处理程序正处于目标对象上，eventPhase=2；
* 冒泡阶段，eventPhase=3；


		var btn = document.getElementById("myBtn");
		document.body.addEventListener("click", function(event){
		    alert(event.eventPhase); //1
		}, true)
		
		btn.onclick = function(event){
		    alert(event.eventPhase); //2
		}
		
		document.body.addEventListener("click", function(event){
		    alert(event.eventPhase); //3
		}, false)
