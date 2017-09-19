---
author: bydiao
comments: true
date: 2013-11-26 07:01:40+00:00
layout: post
title: Zookeeper的基本概念和部署
categories:
- Hadoop
tags: [Hadoop]
---

1.Zookeeper基本概念

Zookeeper是一个针对大型分布式系统的可靠协调系统，提供的功能包括：配置维护、名字服务、分布式锁，分布式同步、组服务等。概念有一些抽象，不过顾名思义，Zookeeper就是hadoop生态系统框架的一个keeper，能帮助解决分布式系统存在的一系列问题。

待续....


2.Zookeeper伪分布式部署


Zookeeper主要需要通过Tcp实现Server间的通信，因此配置Zookeeper，主要是配置各个Server通信的IP和Port。
配置通过修改conf文件夹下的Zoo.cfg文件实现，例如要配置3个Zookeeper Server则配置如下。

将Zookeeper复制三份，分别修改三个zoo.cfg文件

{% highlight C %}
	#zk1
	ckTime=2000
	initLimit=10
	syncLimit=5
	dataDir=/home/diaoboyu/Desktop/Zoo/zk1
	clientPort=2181
	
	server.1=192.168.0.2:2888:3888
	server.2=192.168.0.2:2889:3889
	server.3=192.168.0.2:2890:3890
	

	#zk2
	ckTime=2000
	initLimit=10
	syncLimit=5
	dataDir=/home/diaoboyu/Desktop/Zoo/zk2
	clientPort=2182
	
	server.1=192.168.0.2:2888:3888
	server.2=192.168.0.2:2889:3889
	server.3=192.168.0.2:2890:3890

	#zk3
	ckTime=2000
	initLimit=10
	syncLimit=5
	dataDir=/home/diaoboyu/Desktop/Zoo/zk3
	clientPort=2183

	server.1=192.168.0.2:2888:3888
	server.2=192.168.0.2:2889:3889
	server.3=192.168.0.2:2890:3890
{% endhighlight %}

另一个要注意的是，要确定dataDir的路径是正确的
同时要在dataDir下分别建立一个myid文件，里面包含一个数字，对应自己的Server号码
例如zk1下建立的myid里面，包含一个数字1即可。

配置完成后，要在三个文件夹下分别用脚本启动Zookeeper Server。

完全分布式配置的方式基本相同，只要修改IP和Port等即可。
