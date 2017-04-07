---
layout: post
title: 关于Promise对象
date: 2017/04/07 23:31:04  
categories: Javascript
tag:
---

* content
{:toc}

### 基本用法

```Javascript
var promise = new Promise ( (resolve, reject) => {
    if (异步成功) {
        resolve(value)
    } else {
        reject(error)
    }
} )

promise.then ( (value) => {
    //success
}, ( error ) => {
    //fail
})
```

 - `Promise.prototype.then()`返回的是一个新的Promise对象，可以链式调用
 - `Promise.all()`将多个Promise实例包装成一个新的Promise实例

```Javascript
var P = Promise.all( [p1, p2, p3] );
```

> 1.当`p1`，`p2`，`p3`都是`fullfilled`，`P`状态才会是`fullfilled`，三个实例的返回值组成数组返回给`p`

> 2.当`p1`，`p2`，`p3`中有一个`rejected`，`p`就是`rejected`

 - `Promise.race()`同样将多个Promise实例包装成一个新的Promise实例

```Javascript
var P = Promise.race( [p1, p2, p3] );
```

> 当`p1`， `p2`，`p3`中有一个率先改变状态，`p`就改变，并得到相应的返回值。
