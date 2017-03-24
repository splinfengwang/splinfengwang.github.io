---
layout: post
title:  讲讲闭包和函数执行线程的事儿
date:   2017/03/24 19:52:47  
categories: Javascript
tag:
---

* content
{:toc}

引用阮一峰老师说过的一句话：
> 闭包就是可以读取其他函数内部变量的函数。


```Javascript
    function f1() {
        var n = 999;
        function f2() {
            console.log(n);
        }
        return f2;
    }
    var result = f1();
    result();  //999
```

老师说的没错，就是还有些东西没说完。

> 闭包只能取得包含函数中的任何变量的最后一个值

```Javascript
    for(var i = 0; i < 5; i++){
        setTimeout(function () {
            console.log(i);
        }, 1000)
    }
    //4-4-4-4-4
```

当函数定义完之后，i已经完成运算，最后的一个i=5。一秒之后的console只能取到5；

```Javascript
    for (var i = 0; i < 5; i++) {
        setTimeout((function (i) {
            console.log(i);
        })(i), 1000)
    }
    //0-1-2-3-4
```

这里借助函数参数的按值传递的特征，将每一个i都传了进去实现了值的保存。

---

再来讲讲函数的执行队列，先进先出什么的，好像是这么个说法。
还是上面的例子，做一些小改动。

```Javascript
    for (var i = 0; i < 5; i++) {
        setTimeout((function (i) {
            console.log(i);
        })(i), 0)
    }
    console.log(i);
    //4
    //0-1-2-3-4
```

你看啊，即使setTimeout在上面，还把延迟设成了0；都还是console.log先执行了，这是为啥呢？
其实是这样的，如果有setTimeout在呢，会把其他定义的函数全都执行了，等到队列空闲下来，才把setTimeout塞进去。神奇～～～
