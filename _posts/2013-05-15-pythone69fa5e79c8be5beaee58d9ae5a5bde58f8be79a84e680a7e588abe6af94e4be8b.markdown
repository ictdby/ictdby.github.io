---
author: bydiao
comments: true
date: 2013-05-15 12:35:21+00:00
layout: post
slug: python%e6%9f%a5%e7%9c%8b%e5%be%ae%e5%8d%9a%e5%a5%bd%e5%8f%8b%e7%9a%84%e6%80%a7%e5%88%ab%e6%af%94%e4%be%8b
title: python查看微博好友的性别比例
wordpress_id: 350
categories:
- python
tags: [python]
---

今天用新浪的python sdk查看了自己微博粉丝的性别比例，166男性，52女性，3:1的比例，女性粉丝很少。

主要用到了json解析和基本sdk的应用。

首先要获取某个用户的访问权限，在上一篇博客上已经说明。


	def calcgender():
		pagelength = 50
		friendlist = api.friendships.friends.get(uid='2040433771')
		total = friendlist["total_number"]
		m=0
		f=0
		cursor=0
		while cursor < total:
			friendlist = api.friendships.friends.get(uid='2040433771',cursor=cursor)
			cursor += pagelength
			for u in friendlist["users"]:
				if u["gender"] == "m":
					m += 1
				elif u["gender"] == "f":
					f += 1
			print len(friendlist["users"])
		print m
		print f

新浪微博对SDK有一个统一的接口定义规范，
[http://open.weibo.com/wiki/%E5%BE%AE%E5%8D%9AAPI](http://open.weibo.com/wiki/%E5%BE%AE%E5%8D%9AAPI)
按照这个规范 friendships/friends这个函数在python中应该这样调用：
首先查看类型为get，参数有uid，cursor等

	friendlist = api.friendships.friends.get(uid='2040433771',cursor=cursor)


这样，friendlist中就获取了一系列描述用户分析的json结构体。
json的解析也很简单，相当于字符串为下标的数组。

这样利用以上代码，读懂新浪sdk，就可以统计出自己好友中男性女性共有多少。

这里不仅仅是一个统计应用，还可以将sdk的使用举一反三，做出更多的探索。
