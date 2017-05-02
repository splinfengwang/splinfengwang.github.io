---
layout: post
title: 冒泡和选择排序
date: 2017/04/17 10:31:04  
categories: Javascript
tag:
---

* content
{:toc}

冒泡排序和选择排序在原理上其实是很相似的，算法实现上也是两个循环嵌套，但是实际的区别在哪里呢？

冒泡排序指相邻两个元素进行比较后决定是否交换位置。

选择排序则是指将第一个元素与其他元素比较，选出最大或最小放在第一位，然后将第二个元素与除第一个元素以外的元素（因为第一个元素已经确定了）比较，选出最大或最小放在第二位，依此类推。

#####冒泡算法实现
```Javascript
    const mp = (arr) => {
        let len = arr.length;
        for(let = i = 0; i < len; i++){
            for(let j = 0; j < len - i; j++){
                if(arr[j] < arr[j+1]){ //内循环比较
                    let t = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = t;
                }
            }
        }
        return arr;
    }
```

#####选择算法实现
```Javascript
    const xz = (arr) => {
        let len = arr.length;
        for(let i = 0; i < len-1; i++){
            for(let j = i+1; j < len; j++){
                if(arr[i] < arr[j]){    //内外循环比较
                    let t = arr[i];
                    arr[i] = arr[j];
                    arr[j] = t;
                }
            }
        }
        return arr;
    }
```
