---
layout: post
title: 常见的HTTP缓存控制
date: 2017/04/17 10:31:04  
categories: 网络相关
tag:
---

* content
{:toc}


 - pargma: no-cache;

 > 禁用缓存

 - Expires: Fri.11 Jun 2021 11:33:01 GMT

 > 定一个资源过期时间点，时间为服务器时间

 - Cache-Control:（请求首部）
    - no-cache;

    > 不使用缓存，直接发起请求

    - no-store;

    > 所有内容都不会被保存到缓存或internet临时文件中

    - max-age = delta-seconds;

    > 告知服务器，客户端希望接收到一个存在时间（age）不大于`delta-seconds`秒的资源

    - min-fresh = delta-seconds;

    > 告知服务器，客户端希望接收到一个在小于`delta-seconds`秒内被更新过的资源

 - Cache-Control:（响应首部）
    - public;

    > 表明任何情况下都得缓存该资源

    - no-transform

    > 告知客户端缓存文件时不得对实体数据进行修改

 - Last-Modified: Fri.11 Jun 2021 11:33:01 GMT

 > 客户端与服务端校验资源最后修改的时间，若一致则返回304，不一致则200+新资源

 - ETag: xxxxxxxxxxxxxxxx

 > 同`Last-Modified`，不同在于校验内容为一个唯一标识符，为了解决`Last-Modified`可能存在不准确的问题

#### focus：

1.Expires/Cache-Control:max-age

    前者标记失效时间，可能会因为客户端与服务端时间不一致而受到影响，后者则是失效时间段，可避免这个问题。Expires支持http1.0、1.1，Cache-Control只支持http1.1，所以为了兼容，通常会两个一起写。

2.Last-Modified/ETag

    Last-Modified无法解决一秒内多次修改文件，ETag可以
