---
author: qicfan
comments: true
date: 2011-07-21 09:55:36+00:00
layout: post
slug: '%e8%ae%b0%e5%bd%95php%e4%b8%adinclude%e7%9a%84%e4%b8%80%e4%b8%aa%e5%b0%8f%e7%9f%a5%e8%af%86%e7%82%b9'
title: 记录PHP中include的一个小知识点
wordpress_id: 216
categories:
- php
- 技术杂谈
tags:
- include
- php
---

PHP中inlucde一般是用来包含文件的，他的特点是：可以用在代码分支中，而不是直接加载（require是执行前加载），而且include还有一个最重要的功能是，它具有返回值，你可以像使用一个函数一样使用它，只要在那个文件里有return语句，在调用include的地方就可以接收返回值，代码如下：

a.php:

    
    $a = 100;
    return $a;




b.php:

    
    $c = include("a.php");
    var_dump($c);




这时候我们访问b.php会看到打印出了 int 100

这说明返回值生效了，利用这个特性，我们可以做很多事情！剩下的就在需要的时候去思考吧！
