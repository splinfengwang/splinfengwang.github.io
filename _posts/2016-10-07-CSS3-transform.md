---
layout: post
title: CSS3 —— 变形处理
date:   2016/10/07 12:32:47  
categories: CSS3
tag:
---

* content
{:toc}


# transform功能

---

### 旋转

  * 使用rotate方法：在参数中加入角度值，角度值后面跟表示角度单位的“deg”文字即可。例如

    ```css
    .div1{
        transform:rotateX(50deg);
        transform:rotateY(50deg);
        transform:rotateZ(50deg); //参数为正就是顺时针旋转，负则是逆时针旋转
    }
    //同时由几个旋转时会以最后一个为准，上例就是以rotateZ()为准。
    ```

### 缩放

  * 使用scale方法：实现文字或图像的缩放处理，在参数中指定缩放倍率。例如

    ```css
    div{
        transform: scaleX(0.5); //表示缩小一半
        transform: scaleY(0.5); //表示缩小一半
        transform: scaleZ(0.5); //表示缩小一半
    }
    ```

  * 可以分别指定元素的水平的放大倍率与垂直方向的放大倍率。例如

    ```css
    div{
       transform: scale(0.5, 2); //表示水平缩小一半，垂直方向放大一倍
    }
    ```

### 倾斜

  * 使用skew方法：实现文字或图像的倾斜处理，在参数中分别指定水平方向上的倾斜角度与垂直方向上的倾斜角度。例如

    ```css
    .div1{
        transform: skewX(30deg);
        transform: skewY(30deg);
    }
    .div2{
        transform: skew(30deg, 30deg);
    }
    //两个例子都表示水平和垂直分别倾斜30度，sekw()没有Z轴倾斜
    ```

### 移动

  * 使用translate方法：移动文字或图像，在参数中分别指定水平方向上的移动距离和垂直方向上的移动距离。例如

    ```css
    .div1{
        transform: translateX(50px);
        transform: translateY(50px);
        transform: translateZ(50px);
    }
    .div2{
        transform: translate(50px, 50px, 50px);
    }
    //两个例子都表示水平、垂直和Z轴分别倾斜30度
    ```

### 指定基准点

  * 使用transform-origin属性，可以改变变形的基准点。默认基准点是元素的中心点。例如

    ```css
    div{
        transform-origin: left bottom; //表示左下角为基准点，单一个left指左侧中点
    }
    //“基准点在元素水平方向上的位置”中可以指定的值为left、center、right；
    //“基准点在元素垂直方向上的位置”中可以指定的值为top、center、bottom；
    ```

### 多种变形

  * 可以同时写在一行样式代码中。例如

    ```css
    div{
        transform: rotateX(30deg) translateX(50px) scaleY(0.5);
    }
    ```
