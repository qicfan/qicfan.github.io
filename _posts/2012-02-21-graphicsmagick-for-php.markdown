---
author: qicfan
comments: true
date: 2012-02-21 08:59:02+00:00
layout: post
slug: graphicsmagick-for-php
title: GraphicsMagick for PHP
wordpress_id: 383
categories:
- php
- 技术杂谈
tags:
- gmagick
- GraphicsMagick
- php
---

GraphicsMagick没有测试过，但是项目组要用，就装吧，在linux下没啥特别的，下载源码，编译，如果是64位系统要踩哟个64位编译，修改下configure即可：CFLAGS="-O3 -fPIC" ./configure --enable-shared，然后make && make install就安装完成了

安装完成以后再安装php的gmagick的扩展，也很简单，只要有GraphicsMagick，就基本不报错。

扩展安装完成后，扩展会提供一个Gmagick的php对象用于处理图片，里面提供了很多实用的方法，具体的可以去php手册里看。。

我写好图片处理的方法之后进行了一个简单的测试，发现GraphicsMagick生成的图片并不比GD的更小，也不比GD的质量更好，但是在批量处理图片时优势显示出来了，我生成100张缩略图，GraphicsMagick只用了20s，但是GD却用了30s+，效率差了三分之一，我觉得很多了，这种在大负载下优势是很明显的。

具体的没有做测试，也就不多说了。。。
