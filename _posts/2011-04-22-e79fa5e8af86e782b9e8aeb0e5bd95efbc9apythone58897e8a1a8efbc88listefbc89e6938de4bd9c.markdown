---
author: qicfan
comments: true
date: 2011-04-22 15:19:21+00:00
layout: post
slug: '%e7%9f%a5%e8%af%86%e7%82%b9%e8%ae%b0%e5%bd%95%ef%bc%9apython%e5%88%97%e8%a1%a8%ef%bc%88list%ef%bc%89%e6%93%8d%e4%bd%9c'
title: 知识点记录：python列表（list）操作
wordpress_id: 61
categories:
- python
tags:
- list
- python
---

test_list = ['a', 'b', 'c']

**插入一个元素：append(xxx)**

test_list.append('d')   #输出['a', 'b', 'c', 'd']

test_list.append(['e', 'f'])   # 输出['a', 'b', 'c', ['e', 'f']]



**清空列表：test_list = []    或者test_list[:]  = []**

**删除元素：remove()**

test_list.remove('a')   #输出['b','c']

**查找元素的位置：index('xxx')**

test_list.index('a') # 返回0 如果不存在这个元素，则抛出一个异常


