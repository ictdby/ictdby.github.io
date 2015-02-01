---
author: bydiao
comments: true
date: 2013-05-09 02:20:00+00:00
layout: post
slug: python%e8%8e%b7%e5%8f%96ctrlc%e7%bb%88%e6%ad%a2%e8%bf%9b%e7%a8%8b%e4%b8%ad%e6%96%ad
title: python获取CTRL+C终止进程中断
wordpress_id: 338
categories:
- python
tags: [python]
---

CTRL+C是终止进程快捷键，组合输入后会向程序发出终止进程中断，程序会自动终止执行。

现在要用python获取CTRL+C中断，并在退出前实现需要的一些列操作。例如一个循环读写文件的程序，退出前要将文件内容写回等操作。

具体思路如下：

首先要重载中断响应函数，然后用signal方法将终止进程中断SIGINT绑定到这个函数上

	import signal

	def sigint_handler(signum,frame):
        global is_sigint_up
        is_sigint_up = True
        print 'catched interrup signal'

	signal.signal(signal.SIGINT, sigint_handler)

	is_sigint_up = False


这样当CTRL+C中断到来后，程序就会执行sigint_handler函数。

这里通过一个全局变量实现中断响应函数与主进程函数的通信。is_sigint_up初始为false，中断到来后设置为true，主进程就可以判断is_sigint_up的值来判断是否需要中断自己。

主进程函数实现如下

	def get():

        while True:
                try:
                        pass
                except Exception,e:
                        print "error"

                if is_sigint_up:
                        print "exit"
                        
                        break


这样，就实现了程序响应ctrl+c中断的功能，在程序实现中很有用。
