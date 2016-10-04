---
layout: post
title:  变量类型
date:   2016-10-04 11:27:00 +0800
categories: js笔记
tag: js笔记
---

* content
{:toc}


*每个函数函数都是对象，都会占用内存；内存中的对象越多，性能就越差。必须事先制定所有事件处理程序而导致的DOM访问次数，会延迟整个页面的交互就绪时间。*


事件委托
----------

>对“事件处理程序过多”问题的解决方案就是事件委托。事件委托利用了事件冒泡，只指定一个事件处理程序，就可以管理某一类型的所有事件。

  
	<ul id="myLinks">
	<li id="doSomewhere">doSomewhere</li>
	<li id="goSomething">goSomething</li>
	<li id="sayHi">sayHi</li>
	</ul>
    
    <script>
        var list = document.getElementById("myLinks");
        
        EventUtil.addHandler(list, "click", function(event){
            event = EventUtil.getEvent(event);
            var target = EventUtil.getTarget(event);
            
            switch(target.id){
                case "doSomewhere":
                    document.title = "...";
                    break;
                
                case "goSomewhere":
                    location.herf = "...";
                    break;
                    
                case "sayHi":
                    alert("hi");
                    break;
            }
        })
    </script>
    

上例中，我们使用事件委托只为`<ul>`元素添加了一个onclick事件处理程序。由于所有列表项都是这个元素的子节点，而且它们的事件会冒泡，所以单击事件最终会被这个函数处理。事件目标是被单击的列表项，因而可以通过检测id属性来决定采取适当的操作。
    

移除事件处理程序
===========  
>对“事件处理程序过多”问题的另一种解决方案就是在不需要的时候移除事件处理程序。因为内存中留有那些过时不用的“空事件处理程序”（dangling event handler），也是造成WEB应用程序内存与性能问题的主要原因


    <div id="myDiv">
        <input type="button" value="click me" id="myBtn">
    </div>

	<script>
	var btn = document.getElementById("myBtn");
	btn.onclick = function(event){
    ......
    btn.onclick = null; //移除事件处理程序
    document.getElementById("myDiv").innerHTML = "processing...";
	};
	</script>
	
测试
-------------
>在上例中，我们在程序执行完毕之后，移除元素之前先把执行程序销毁了，避免“空事件处理程序”造成内存问题。