---
layout: post
title:  变量类型
date:   2016/10/4 16:12:47  
categories: Javascript
tag: 变量、作用域和内存问题
---

* content
{:toc}


* 基本类型：指简单的数据段；

    基本数据类型是按值访问的，因为可以操作保存在变量中的实际值；
    
* 引用类型：指的是那些可能有多个值构成的对象；

    javascript不允许直接访问内存中的位置，也就是说不能直接操作对象的内存空间。在操作对象时，实际上是在操作对象的引用而不是实际的对象。为此，引用类型的值是按引用访问的。严谨地说，当复制保存着对象的某个变量时，操作的是对象的引用。但在为对象添加属性时，操作的是实际的对象。


### 动态的属性
    
* 定义基本类型值和引用类型值得方式是类似的：创建一个变量并为该变量赋值。
* 对不同类型值可以执行的操作大相径庭。
* 对于引用类型的值，我们可以添加、删除和修改其属性和方法。
		
		var person = new Object();
		person.name = "Nick";
		alert(person.name); //"Nick"

	> 这个例子创建了一个对象并将其保存在变量person中。然后，我们为该对象添加了一个名为name的属性。紧接着，有通过`alert()`函数访问了这个新属性。

### 复制变量值

* 在从一个变量向另一个变量复制基本类型值和引用类型值时，存在不同
* 如果从一个变量向另一个变量复制基本类型值，会在变量对象上创建一个新值，然后把该值复制到为新变量分配的位置上。
		
		var num = 5;
		var num1 = num;
	
	> 这个例子中，num和num1保存的值是都5,但是两者的值是完全独立的，num1是num的一个副本。两个变量可以参与任何操作而不会互相影响。

* 当一个变量向另一个变量复制引用类型的值时。同样也会将存储在变量对象中的值复制一份放到为新变量分配的空间中。不同的是这个值的副本其实是一个指针，而这个指针指向存储在堆中的一个对象。复制操作结束后，两个变量实际上将引用同一个对象。因此，改变其中一个变量，就会影响另一个变量。
		
		var obj1 = new Object();
		var obj2 = obj1;
		obj1.name = "Nick";
		alert(obj2.name); //"Nick"

	>在这个例子中，两个变量会相互影响，因为都是引用同一个对象。

### 传递参数

* 在向参数传递基本类型的值时，被传递的值会被复制给一个局部变量（即命名参数，或者是arguments对象中的一个元素）。

		function addTen = function(num){
			num += 10;
			return num;
		}
		var count = 20;
		var result = addTen(count);
		alert(count); //20
		alert(result); //30
	
	> 在调用这个函数时，变量count作为参数被传递给函数，这个变量的值是20。于是，数值20被复制给参数num以便在`addTen()`中使用。在函数内部，参数num的值被加上了，但这一变化不会影响到函数外部的count变量。

* 在向参数传递引用类型的值时，会把这个值在内存中的地址复制给一个局部变量，因此这个局部变量的变化就会反映在函数的外部。

		function setName(obj){
			obj.name = "Nick";
		}
		
		var person = new Object();
		setName(person);
		alert(person.name); //"Nick"
	
	> 这个例子中创建了一个对象，并将其保存在了变量person中。然后这个变量被传递到`setName()`函数中被复制给了obj。在这个函数内部，obj和person引用的是同一个对象，即使这个变量是按值传递的，obj也会按引用来访问同一个对象。于是，当在函数内部为obj添加name属性后，函数外部的person也将有所反映，因为person指向的对象在堆内存中只有一个，而且是全局对象。
	
		function setName(obj){
			obj.name = "Nick";
			obj = new Object();
			obj.name = "Mike";
		}
		
		var person = new Object();
		setName(person);
		alert(person.name); //"Nick"

	> 这个例子在函数中重新定义了一个对象，并为该对象定义了一个带有不同值的name属性。但是结果表明，即使在函数内部修改了参数值，原始的引用仍旧不变。实际上，当在函数内部重写obj时，这个变量的引用就是一个局部对象了。而这个局部对象会在函数执行完毕后立即被销毁。
	
### 检测类型

* 检测基本数据类型，使用`typeof`操作符。

		var s = "Nick";
		var b = true;
		var i = 22;
		var u;
		var n = null;
		var o = new Object();
		
		alert(typeof s);//string
		alert(typeof b);//number
		alert(typeof i);//boolean
		alert(typeof u);//undefind
		alert(typeof n);//object
		alert(typeof o);//object

* 检测引用数据类型，使用`instanceof`操作符。

		alert(person instanceof Object);//变量person是object吗？
		alert(colors instanceof Array);//变量colors是array吗？
		alert(pattern instanceof RegExp);//变量pattern是regexp吗？
	
	>根据规定，所有引用类型的值都是Object的实例。因此，在检测一个引用类型之和Object构造函数是，`instanceof`操作符始终会返回true。