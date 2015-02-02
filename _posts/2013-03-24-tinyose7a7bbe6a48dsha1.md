---
author: bydiao
comments: true
date: 2013-03-24 15:18:08+00:00
layout: post
slug: tinyos%e7%a7%bb%e6%a4%8dsha1
title: TinyOS移植Sha1小结
wordpress_id: 246
categories: [Windows编程&.NET]
tags: [Wireless Sensor Network]
---

一篇论文的实验，需要将sha1算法移植到telosb上，且不说sha1是个什么东西，只关注如何将纯c代码移植为telosb平台下的nesC。

首先要总结一下这次移植过程中的tinyos通用经验，然后简单记录一下移植过程

1.tinyos的文件夹结构

tinyos-2.1.1目录下主要有
apps：
一些已经写好的tinyos应用，都是可以借鉴的例子程序，包括Blink，Basestation，BlinkToRadio等，基本涵盖了tinyos的编程举例。
support：
包含了makerules，以及java，c/c++,python协同编程的支持。
tos：
系统内核组件等，是最终要的文件夹
/tos/interface  所有接口的声明
/tos/system     系统内核组件，是tinyos运行时所必须的组件
/tos/platforms/ 特定节点平台的代码，与芯片本身无关
/tos/libs/      包含接口和组件等，是扩展组件
/tos/types/     头文件，类型定义文件夹

2.组件如何provides一个interface
一个interface，必须要由一个component provides声明，才能被其他component使用。一个interface就像是一个类，一个component就像是一个类的集合。interface中可以定义commond，就像是定义了一个类方法。
自定义一个interface一定会有更好的方法，现只总结一下我实现的方法。

假设接口名为Test
在/tos/system下，创建一个TestC.nc，一个TestP.nc,这就构成了一个基本的组件。TestC.nc为顶层configuration，TestP.nc为module实现。

    //TestC.nc
    configuration TestC
    {
        provides interface Test;
    }
    implementation
    {
        components TestP;

        test = TestP;
    }



    //TestP.nc
    module TestP
    {
        provides interface Test;
    }
    implementation
    {
        command void cmd1()
        {
         //....
        }
    }            

同时，要在/tos/interface下对接口进行声明

    #include "test.h"//如果需要有头文件，可以放到/tos/types文件夹下
    interface test
    {
        command void cmd1();
    }

这样，一个interface就定义完成了，实现函数体，就可以在其他component中使用test的方法了。

3.头文件如何引用

如2中所说，自定义的头文件，如果不修改makefile，可以直接放在/tos/types/中，系统自动调用。

4.telosb与X86不同

纯C代码可以运行在X86的PC上，转化为nesC，有时候也不能完全运行在telosb上，telosb的处理器是16位的MSP430,8MHZ，10KB RAM。在这次代码移植中，遇到了这洋一个问题：

    uint32_t w = 0;
    uint8_t b = 0x03;
    w = b << 24;

如果是X86，代码w的结果为0x03000000，毫无争议，但到了16位的MSP430上，结果就是0x00000000，原因很简单，16位的cpu，左移16位就变成0了。类似这样微操作的问题应该会是纯C向nesC移植的障碍之一。
上述代码可以做以下修改

    uint32_t w = 0;
    uint8_t b = 0x03;
    w = b;
    w = w << 24;


5.移植过程
sha1算法是一个加密中会用到的hash算法，一个sha1算法流程主要包括以下三步:
shaRest()//初始化数据结构
shaInput()//处理输入
shaResult()//获取结果
随将sha写为一个组件，向外提供一个sha接口，另写一个shaTestApp，调用此接口。
在Boot.boot()中，调用以上三个方法，则可得到一组sha的输出。
按此思路，期间处理一些小细节，即可移植成功。
