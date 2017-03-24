---
layout: post
title:  关于window的location对象
date:   2017/03/24 21:52:47  
categories: Javascript
tag:
---

* content
{:toc}

比如页面的链接是这个样子的：
`http://www.wrox.com:8080/WlieyCDA/index.htm#content?q=javascript`

```Javascript
    window.hash;    //"#content"
    window.host;    //"www.worx.com:8080"
    window.hostname;    //"www.worx.com"
    window.href;    //"http://www.wrox.com:8080/WlieyCDA/index.htm#content?q=javascript"
    window.pathname;    //"/WlieyCDA/index.htm"
    window.port;    //"8080"
    window.protocol;    //"http"
    window.search;  //"?q=javascript"
```
