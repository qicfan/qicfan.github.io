---
author: qicfan
comments: true
date: 2012-01-16 04:14:12+00:00
layout: post
slug: hessian%e5%9c%a8php%e4%b8%ad%e7%9a%84%e4%bd%bf%e7%94%a8
title: Hessian在php中的使用
wordpress_id: 369
categories:
- php
- 技术杂谈
tags:
- Hessian
- HessianPHP
- php
---

最近因为要跟java那边的同事开发的一个中心进行对接，所以使用到了hessian，以前还真没听说过它，后来google了下，发现这是一个http协议上的接口协议（远程方法调用），比较好的是网上有PHP的实现版本，不用自己折腾了，不过貌似很久没更新过了。

具体在使用过程中确实发现了一些问题，第一个就是PHP包中有两个版本，一个Hessian1，一个Hessian2，貌似这两个版本跟Server端的Hessian版本有关系，默认是使用的Hessian2，但是我这里会报错，所以我改成了Hessian1,具体就是在实例化时传入一个version参数：

    
    /**
     * version表示使用Hessian1，saveRaw表示保存返回的原始数据（便于调试）
     */
    $handler = new HessianClient ( $this->getUrl (), array ('version' => 1, 'saveRaw' => TRUE ) );


改好之后调用又发现了问题，比如我这样一个方法addGoods(long goodsId, string cateId)，在php中由于是弱类型，所以我直接就使用了一些函数的返回值，没想到到JAVA那边就出现了问题，hessian服务无法解析这个请求的内容，报错信息如下：
java.io.IOException: expected 'c' in hessian input at 72
我的解决方法是一一对照参数类型，确保传递时的参数是需要的类型，如我上面的addGoods方法，第二个cateId是string类型，但是php中确是int型，因为没有显式的转换过，所以id基本都是Int型，之需要做如下处理即可:

    
    $goodsId = (int)$goodsId;
    $cateId = (string)$cateId;


这么修改过后，参数类型一致，调用也就没有问题了，关于调休可以看看hessianphp的源码自己进行。

