---
author: qicfan
comments: true
date: 2011-05-11 09:21:46+00:00
layout: post
slug: '%e5%9c%a8ubuntu%e4%b8%8b%e5%ae%89%e8%a3%85eclipsepydevphpandroid%e7%9a%84%e5%bc%80%e5%8f%91%e7%8e%af%e5%a2%83'
title: 在ubuntu下安装eclipse+pydev+php+android的开发环境
wordpress_id: 167
categories:
- php
- python
- 技术杂谈
tags:
- android
- eclipse
- php
- pydev
---

昨天安装了ubuntu的11.04版本，然后在ubuntu软件中心安装了eclipse，然后就想着怎么给它配上PHP、PYTHON、ANDROID的开发环境，今天开始着手捣鼓，弄了差不多一天总算成功了，万恶的墙啊！！

言归正传，eclipse就是用ubuntu软件中心提供的galileo版本，先安装php插件：

1、打开help->Install new software

2、在新窗口中的work with后面的文本框中输入：http://download.eclipse.org/eclipse/downloads/，然后回车

3、在下面的列表中选择Program，然后选择php developer for eclipse之类的，如果想要支持c/c++，也可以选上c/c++那一项

4、然后下一步，会提示你都要安装什么，如果需要可能要选择I agree之类的，然后点击finish

5、自动安装完成（如果没有背墙，网速足够的话，否则可能会出错误）

6、在window->preferences->php中添加php的debugger，具体请大家自己看看吧

好了，PHP插件安装完成，然后是python，我们选择pydev，流程类似上面，只不过这回仓库地址是：http://pydev.org/updates，安装完成后，需要设置python库的路径，这个就不详细说了，很好找

然后安装android sdk和adt插件，由于android官网被墙了，我们需要翻下墙，才能下载到sdk，翻墙不说了，具体下载地址是：http://developer.android.com/sdk/index.html，在这个页面选择自己的系统版本下载

adt插件的安装同上面的两个插件安装类似，仓库URL地址是：https://dl-ssl.google.com/android/eclipse/，安装完成后需要在window->preferences->andorid里设置sdk的路径，然后就OK了。



上面配置了一个常用的集成开发环境，虽然eclipse比较庞大，功耗也很大，但是胜在方便（对emacs之类实在是不熟悉）。
