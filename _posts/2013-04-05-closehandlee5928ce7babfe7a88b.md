---
author: bydiao
comments: true
date: 2013-04-05 07:47:10+00:00
layout: post
slug: closehandle%e5%92%8c%e7%ba%bf%e7%a8%8b
title: CloseHandle()和线程
wordpress_id: 285
categories:
- 面试题
tags: [面试题]
---

从学操作系统到现在，对CloseHandle()的理解一直不甚，尤其是CloseHandle()与线程配合使用的时候，例如以下代码：


    ThreadHandle = CreateThread(NULL,0,.....);
    CloseHandel(ThreadHandle );


建立一个线程，然后关闭了这个线程的句柄，那不就是停止了这个线程了吗。显然，这种错误的理解一直被怀疑，但始终未被校正。

首先说一下CloseHandle()函数的作用，顾名思义，这个函数是关闭了一个Handle，中文译为"句柄"(不知道为什么这么翻译)。

句柄为何物，简单的讲，可以认为是一个索引，Windows的窗口，信号量，线程等都会对应一个句柄，反过来说，任何一个Windows进程，都会有一个句柄列表，指向该进程所述的内核对象，如窗口，信号量，线程等等。

句柄的作用，一是可以通过句柄作为索引，对内核对象进行相关操作，功能类似一个指针。而是标记了内核对象的生死，一个内核对象可以有被对个句柄索引，当它的索引数为0时，系统会干掉这个内核对象。

回过头再说CloseHandle函数与线程的操作，当我们CreateThread的时候，系统会为这个线程创建一个句柄，同时会返回一个句柄供用户进行后续操作，如WaitForSingleObject等。如果用户没有对该进程的后续操作，应该将这个句柄Close掉。因为此时，被创建的线程句柄索引数为2，线程执行完以后会变为1，系统不会对线程资源进行清理，造成线程驻留，句柄泄露等问题。因此有必要将CreateThread返回的Handle关掉。

关掉了这个句柄，不会影响线程的执行。
很多从课堂听来的知识和概念都很难理解的很透彻
You hear and you forget ;You do and you understand。
