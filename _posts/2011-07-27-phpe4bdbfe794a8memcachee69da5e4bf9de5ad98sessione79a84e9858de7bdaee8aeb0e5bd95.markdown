---
author: qicfan
comments: true
date: 2011-07-27 08:50:38+00:00
layout: post
slug: php%e4%bd%bf%e7%94%a8memcache%e6%9d%a5%e4%bf%9d%e5%ad%98session%e7%9a%84%e9%85%8d%e7%bd%ae%e8%ae%b0%e5%bd%95
title: php使用memcache来保存session的配置记录
wordpress_id: 235
categories:
- php
tags:
- memcached
- php
- save_handle
- save_path
- session
---

以前在就使用过memcache来存储PHP的session,所以一直没有注意其中的一些细节，今天给自己的笔记本重装了ubuntu，配置PHP环境的时候，PHP的memcache扩展使用了php_memcached而不是php_memcache，然后打开以前做的一个项目的时候，问题出现了，提示:
Warning: ini_set() [function.ini-set]: Cannot find save handler 'memcache'，看到这个错误，我以为是memcached安装出现了问题，检查了下，发现memcached可以正常使用，于是GOOGLE之，发现一篇博文里有提到这个事情，说是php_memcache和php_memcached的差异造成的。
如果安装的是php_memcache扩展那么在php.ini中设置的是这样：
session.save_handle = memcache
session.save_path = tcp://217.0.0.1:11211
如果安装的是php_memcached扩展设置就需要改成这样：
session.save_handle = memcached
session.save_path = 127.0.0.1:11211

特此记录一下，等有时间测试下多台memcached服务器的设置。。。
