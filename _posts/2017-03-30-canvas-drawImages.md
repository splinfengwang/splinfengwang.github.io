---
layout: post
title:  在canvas中引入一张图片并绘制
date:   2017/03/30 17:52:47  
categories: javascript
tag:
---

```Javascript
    let canvas = document.getElementById('canvas');
    if (canvas.getContext) {
        let ctx = canvas.getContext('2d');
        let img = new Image();
        img.addEventListener('load', function () {
            ctx.drawImage(img, 0, 0);
        })
        img.src = 'xxx/xxxx/xxx.png'
    }

```
