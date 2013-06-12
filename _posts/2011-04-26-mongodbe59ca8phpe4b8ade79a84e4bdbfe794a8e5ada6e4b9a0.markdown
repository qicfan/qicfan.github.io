---
author: qicfan
comments: true
date: 2011-04-26 09:15:22+00:00
layout: post
slug: mongodb%e5%9c%a8php%e4%b8%ad%e7%9a%84%e4%bd%bf%e7%94%a8%e5%ad%a6%e4%b9%a0
title: mongodb在php中的使用学习
wordpress_id: 85
categories:
- php
tags:
- mongodb
- php
---

最近一直在看mongodb的相关内容，下午无事的时候就准备看看是否可以将mongodb用在文章的评论中，所以就在本地搭建了一下测试环境，先进性一些简单的测试，看看在php中的用法

安装启动好mongodb，然后安装好php_mongo扩展，具体参见：[http://cn.php.net/mongo](http://cn.php.net/mongo)

    
    $m = new Mongo("10.69.10.100");
    $db = $m->comment;
    $key = md5("17954");
    $col = $db->$key;
    $comment = array('author'=>'zeroq', 'timeline'=>1232312123, 'type'=>'Article', 'content'=>'Hello World', 'body_id'=>17954, 'body_title'=>'这是一篇文章');
    $col->insert($comment);
    $cursor = $col->findOne();
    print $cursor;


运行后抛出异常：
PHP Fatal error: Uncaught exception 'MongoException' with message 'non-utf8 string: 这是一篇文章' in D:\www\test.php:7
Stack trace:
#0 D:\www\test.php(7): MongoCollection->insert(Array)
#1 {main}
thrown in D:\www\test.php on line 7
经过GOOGLE之后发现，这是因为在mangodb中所有的字符串必须是UTF8编码，然后将文件编码转换成UTF-8之后，执行通过。。
简单的代码演示了mongodb的增、改、查（删除很容易）:

    
    $m = new Mongo("10.69.10.100");
    $db = $m--->comment;
    //print_r($db);exit();
    $key = md5("17954");
    $col = $db->$key;
    //$col->remove();exit();
    //$comment = array('author'=>'zeroq', 'timeline'=>time(), 'type'=>'Article', 'content'=>'Hello World again', 'body_id'=>17954, 'body_title'=>'这是一篇文章', 'status'=>0);
    //$col->insert($comment);
    $cursor = $col->find(array("tag"=>"17954"));
    $cursor->sort(array('timeline'=>-1));
    $cursor->limit(2);
    foreach ($cursor as $item) {
    	//$item['tag'] = array('文章', '评论', '17954');
    	//$col->save($item);
    	print_r($item);
    }


刚刚又看了下评论的功能，觉得用mongodb还是比较合适的，将每个文章的评论作为一个集合，每个评论是一个文档，用文章ID的MD5值做为collection的名字。
每个IP针对每一篇文章，在1分钟内只能发表一次，这个记录可以放在memcache中，设置1分钟到期
这样完全摒弃了数据库的低效，在效率上应该会高不少
最起码每个文章的评论集合之间现在没啥关系，不会出现无谓的全表检索
最主要的是方便了对象操作


