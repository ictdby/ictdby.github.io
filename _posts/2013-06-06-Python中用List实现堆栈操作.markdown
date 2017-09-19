---
author: bydiao
comments: true
date: 2013-06-06 08:08:25+00:00
layout: post
slug: python%e4%b8%ad%e7%94%a8list%e5%ae%9e%e7%8e%b0%e5%a0%86%e6%a0%88%e6%93%8d%e4%bd%9c
title: Python中用List实现堆栈操作
wordpress_id: 376
categories:
- python
tags:
- python
---

python中的内置数据类型非常丰富，至少和STL一样强大。

其中list和dictionary好比是内置类型的双子星，被广泛的应用在各种地方。

list可以实现简单的堆栈操作，具体如下：


	"""list as stack"""

	>>> a = [1,2,3,4,5,6]
	>>> a.append(5)   #push
	>>> a
	[1, 2, 3, 4, 5, 6, 5]
	>>> a.pop()       #pop
	5	
	>>> a
	[1, 2, 3, 4, 5, 6]
	>>> 


	"""list as queue"""
	>>> from collections import deque
	>>> a = deque([1,2,3,4,5,6,])  #double queue
	>>> a
	deque([1, 2, 3, 4, 5, 6])
	>>> a.append(5)               #push back
	>>> a
	deque([1, 2, 3, 4, 5, 6, 5])
	>>> a.popleft()              #pop head
	1
	>>> a
	deque([2, 3, 4, 5, 6, 5])
	>>> 

以上就是list实现堆栈的过程，摘自python的教程
python的教程和库都有很好的支持
具体可以访问
python标准库
[http://docs.python.org/2/library/index.html

python教程
[http://docs.python.org/2/tutorial/index.html

