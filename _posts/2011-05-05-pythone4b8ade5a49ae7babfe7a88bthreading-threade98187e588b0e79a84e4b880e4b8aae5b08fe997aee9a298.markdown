---
author: qicfan
comments: true
date: 2011-05-05 05:34:52+00:00
layout: post
slug: python%e4%b8%ad%e5%a4%9a%e7%ba%bf%e7%a8%8bthreading-thread%e9%81%87%e5%88%b0%e7%9a%84%e4%b8%80%e4%b8%aa%e5%b0%8f%e9%97%ae%e9%a2%98
title: python中多线程Threading.Thread遇到的一个小问题
wordpress_id: 153
categories:
- python
tags:
- python
- Threading
- 多线程
---

先看代码

    
    def thread_parse(site):
    	global db
    	site_handle = globals()[site['class']](site, db)
    	site_handle.find_product_from_files();
    	return
    
    thread_pool = []
    sites = [{'name':'xxx', 'url':'xxx', 'class':'xxx', 'site':'xxx', 'area':'xxx'}, {'name':'xxx', 'url':'xxx', 'class':'xxx', 'site':'xxx', 'area':'xxx'}, {'name':'xxx', 'url':'xxx', 'class':'xxx', 'site':'xxx', 'area':'xxx'}]
    for site in sites:
    	th = threading.Thread(target=thread_parse,args=(site));
    	th.start()
    	thread_pool.append(th)
    for ts in thread_pool:
    	threading.Thread.join(ts)


上面的代码是创建了N个线程来同时处理sites列表的数据，在执行时报错说：
thread_parse只需要一个参数，却给了5个

在上面的代码中，参数site是一个字典，(site)应该可以表示为一个元组，事实上也确实成为了一个元组，但是不知道为什么，Thread将site解析成了元组中的5个元素，比较郁闷，暂时没有时间去看源码，只能绕道解决，代码如下：

    
    def thread_parse(site, db):
    	site_handle = globals()[site['class']](site, db)
    	site_handle.find_product_from_files();
    	return
    
    thread_pool = []
    sites = [{'name':'xxx', 'url':'xxx', 'class':'xxx', 'site':'xxx', 'area':'xxx'}, {'name':'xxx', 'url':'xxx', 'class':'xxx', 'site':'xxx', 'area':'xxx'}, {'name':'xxx', 'url':'xxx', 'class':'xxx', 'site':'xxx', 'area':'xxx'}]
    for site in sites:
    	th = threading.Thread(target=thread_parse,args=(site, db));
    	th.start()
    	thread_pool.append(th)
    for ts in thread_pool:
    	threading.Thread.join(ts)


修改后的代码，将thread_parse需要使用的一个global变量db，作为参数传入；这样args就成了具有两个元素的元组，经测试正常！

**Tip:**

经过最近的学习使用，发现tuple如果写成(a)会被解析成a，而写成(a, )才会被作为一个tuple，特此备注，也解释了上面那个问题，答案其实很简单

    
    th = threading.Thread(target=thread_parse,args=(site, ));



