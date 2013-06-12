---
author: qicfan
comments: true
date: 2011-09-01 09:13:53+00:00
layout: post
slug: svn-propset%e4%bd%bf%e7%94%a8
title: svn propset使用
wordpress_id: 265
categories:
- 技术杂谈
tags:
- propset
- svn
- svn propset
- svn:keywords
---

有时候我们想自动将SVN得版本信息，操作人，时间等插入PHP代码中，这时候我们可以这么来操作，在PHP代码得指定部位插入$Id$占位符，然后执行svn propset svn:keywords "Id" filename，以后每次commit之后，都会将最新的版本信息替换$Id$占位符，效果如下：

处理前：

/*
* @author qicfan
*
* @version $Id$
*
*/

处理后：

/*
* @author qicfan
*
* @version $Id: RepairCityCommand.php 13297 2011-09-01 08:40:54Z qixiaopeng $
*
*/
