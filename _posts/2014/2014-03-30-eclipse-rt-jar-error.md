---
layout: post
title: Eclipse无法编译rt.jar中的某些包解决办法
categories: eclipse
tags: 
- eclipse
- rt.jar
---


## Eclipse 最近在写一些代码的时候发现如果引用了rt.jar中的某些包
例如：

    import sun.misc.BASE64Decoder 
    import com.sun.net.httpserver.Headers;



出现错误提示为：Access restriction:   
The type BASE64Decoder is not accessible due to restriction on required library D:/Java/jre/lib/rt.jar 

解决办法如下：

1. Open project properties
2. Select Java Build Path node
3. Select Libraries tab
4. Remove JRE System Library 一次
5. 再次 Add Library JRE System Library

## Eclipse 编译运行时无法加载主类的解决方法
1. auto compile
2. 修改每个java文件(比如加一行，再减一行)，触发使其重新编译
3. OK