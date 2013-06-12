---
author: qicfan
comments: true
date: 2011-04-29 08:49:17+00:00
layout: post
slug: '%e5%9b%a2%e8%b4%ad%e5%af%bc%e8%88%aa%e5%ae%9e%e7%8e%b0%ef%bc%88%e4%b8%89%ef%bc%89'
title: 团购导航实现（三）
wordpress_id: 138
categories:
- python
- 技术杂谈
tags:
- python
- 团购导航
---

经过两天的测试，发现了一些问题有待修正：



	
  1. 分析器改为多线程方式，这样会提高效率，并且会将连续出现某个站点的产品的情况减少

	
  2. 地区属性在分析器中获取，而不是外部指定（需要更改分析器规则，待定）

	
  3. 地区属性支持通配符*，来匹配全国性产品

	
  4. 图片的本地化存储以及缩略图




暂时先写这么多，欢迎大家交流spider和parser的相关问题，也请大家期待我这个小产品。。
