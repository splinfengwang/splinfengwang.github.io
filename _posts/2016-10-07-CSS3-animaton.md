---
layout: post
title: CSS3 —— 动画功能
date:   2016/10/07 16:53:04  
categories: CSS3
tag:
---

* content
{:toc}


> CSS3中的动画功能分为Transitions功能和Animations功能，这两种功能都可以通过改变CSS中的属性值来产生动画效果。
>>Transitions功能支持从一个属性值平滑过渡到另一个属性值.
>>Animations功能支持通过关键帧的指定来在页面上产生更负责的动画效果。

# Transitions功能

***

### 使用方法：transition: property duration timing-function
  * property：表示对哪个属性进行平滑过渡；
  * duration：表示在多久时间内完成属性值的平滑过渡；
  * timing-function：表示通过什么方法进行平滑过渡；
  * 只能指定属性的开始值和终点值，然后在这两个属性值之间实现平滑过渡，不能实现更为复杂的动画效果。

```html
<div>示例文字</div>
```
```css
div{
    background-color: #ffff00;
    transition: background-color 1s linear;
}
div:hover{
    background-color: #00ffff;
}
```
例子中有一个div元素，背景为黄色，通过hover属性指定当鼠标标签停留在div元素上时的背景色为浅蓝色，通过transitions属性指定：当鼠标指针移动到div元素上时，在1秒内让div元素的背景色从黄色平滑过渡到浅蓝色。

```css
拓展写法
div{
    background-color: #ffff00;
    transition-duration: : background-color;
    transition-duration: : 1s;
    transition-timing-function: linear;
    transition-delay: 1s; //该属性指定变换动画特效延迟多久后开始执行，或者写在transition属性第四个参数。
}

div:hover{
    background-color: #00ffff;
}
```

### 同时过渡多个属性值
  * 按照property duration timing-function的格式，每个属性动画用逗号隔开，则会同时进行。

```html
<div>示例文字</div>
```
```css
div{
        background-color: #ffff00;
        color: #000000;
        width: 300px;
        transition:  background-color 1s linear, color 1s linear, width 1s linear;
}
div:hover{
        background-color: #003366;
        color: #ffffff;
        width: 400px;
}
```

# Animations功能

***

### 使用方法：
  * animation-name：指定关键帧集合的名称；
  * animation-duration：指定完成整个动画所花费的时间；
  * animation-timing-function：指定实现动画的方法；
  * animation-delay：用于指定延迟多少秒或多少毫秒后开始执行动画；
  * animation-iteration-count：指定动画的执行次数，可指定为infinite（无限次）；
  * animation-direction：指定动画的执行方向。可指定的属性包括：
      * normal：初始值（动画执行完毕后返回初始状态）。
      * alternate：交替更改动画的执行方向。
      * reverse：反方向执行动画。
      * alternate-reverse：从反方向开始交替更改动画的执行方向。
  * 在一行样式代码中定义animation动画时采用如下所示的书写方式

    >animation:keyframe的名称 动画的执行市场 动画的实现方法 延迟多少秒后开始执行动画 动画的执行次数 动画的执行方向

```html
<div>示例文字</div>
```

```css
div{
    background-color: red;
}
@keyframes mycolor{ //创建关键帧的集合
    0%{
           background-color: red; //关键帧的样式代码
    }
    40%{
            background-color: darkblue;
    }
    70%{
            background-color: yellow;
    }
    100%{
            background-color: red;
    }
}
div:hover{ //使用关键帧集合
        animation-name: mycolor;
        animation-duration: 5s;
        animation-timing-function: linear;
}
```

> 上例实现的动画中带有如下几个关键帧：
    - 开始帧：0%，红色背景；
    - 关键帧：40%，深蓝色背景；
    - 关键帧：70%，黄色背景；
    - 结束帧：100%，红色背景。

### 多个属性同时改变的动画

  * 在关键帧中添加多行样式代码

```css
@keyframes mycolor{
    0%{
           background-color: red;
           transform: rotate(0deg);
    }
    40%{
            background-color: darkblue;
            transform: rotate(30deg);
    }
    70%{
            background-color: yellow;
            transform: rotate(-30deg);
    }
    100%{
            background-color: red;
            transform: rotate(0deg);
    }
}
```

### 实现动画的属性

方法 | 属性值的变化速度
---|---
linear | 在动画开始时与结束时以同样速度进行改变
ease-in | 动画开始时速度很慢，然后速度沿曲线值进行加快
ease-out | 动画开始时速度很快，然后速度沿曲线值进行放慢
ease | 动画开始时速度很慢，然后速度沿曲线值进行加快，然后再沿曲线值进行放慢
ease-in-out | 动画开始时速度很慢，然后速度沿曲线值进行加快，然后再沿曲线值进行放慢
