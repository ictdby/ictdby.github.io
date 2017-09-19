---
layout: post
title: VBF在Aqua-Sim(NS2)的实现
categories: [WSN]
tags:
- ns2
- Aqua-sim
- UWSN
---
### VBF算法概述 ###

### NS2仿真基本思路 ###
NS2的仿真一般分四个步骤，修改此等C++代码，写TCL脚本进行仿真，awk数据处理，gplot出图。
一个一个来说

#### 1. 修改底层C++代码 ####
修改底层C++代码，一般需要继承Agent类建立一个新类
类中要实现recv，command两个虚函数
类中实现各种算法，根据需要仿真的协议栈层次设定
路由层以上的，在Agent里实现即可。
实现类之后，要通过bind函数，把TCL可配置的属性暴露出来。

修改一些配置文件，具体可参考Aqua的教程，或者于斌的NS2教程
修改完成后，重新编译，就可以在TCL中引用自己定义的新协议了

{% highlight c++ %}
set a_(4) [new Agent/NewProName]
$ns_ attach-agent $node_(4) $a_(4)
{% endhighlight %}

#### 2.创建TCL脚本 ####
TCL脚本是仿真的核心，每一个仿真都对应一个TCL，在TCL中，主要做这样几件事
* 配置节点属性，包括各层协议，能量模型，收发能耗，位置，是否移动等等
* 配置网络拓扑，包括托普范围，节点个数等
* 配置Source和Sink，Source还需要定义data_rate_
* 根据协议配置各种属性参数，例如协议中的一些预设变量等
* 配置时序信息，何时开始启动，何时停止，停止后的操作等
* 配置输出，主要是离散事件输出，每一个动作的输出，每一个动作后的状态输出，可根据需要的参数进行配置和输出

TCL脚本非常复杂，要对协议非常了解才能配置好，基本的思路就是这样，总结起来就是两块，属性配置和时序配置

#### 3. awk数据处理 ####
tcl输出的主要文件是xxx.tr文件，可根据这个文件分析诸多参数，要明确各列的参数含义，以及awk的基本操作。

awk的操作可参考酷壳的博客文章[AWK使用](http://coolshell.cn/articles/9070.html)
待研究

#### 4. gplot出图 ####
待研究

### Aqua-Sim的几个类实现 ###

Aqua-Sim的内核仍然是NS2，其运转核心是Scheduler类，核心函数如下

{% highlight C++ %}
void
Scheduler::run()
{
	instance_ = this;
	Event *p;
	/*
	 * The order is significant: if halted_ is checked later,
	 * event p could be lost when the simulator resumes.
	 * Patch by Thomas Kaemer <Thomas.Kaemer@eas.iis.fhg.de>.
	 */
	while (!halted_ && (p = deque())) {
		dispatch(p, p->time_);
	}
}
{% endhighlight %}

套用雪国列车里的概念，这就是一架永动机。


Aqua-Sim是网络仿真的一种，那就离不开协议栈，Aque-Sim主要的工作就是加入了多种水下协议的协议栈实现包。


在underwatersensor/uw_mac中
物理层，

* 实现underwaterphy，水声通信类
* 实现underwaterChannelClass，水声信道模型类
* 实现underwaterPropagation，水声传播模型类

MAC层，

* 实现underwatermac，基本mac类
* 实现tmac等mac类

在underwatersensor/uw_routing中

* 实现uwflooding，洪泛路由
* 实现vectorbasedforward，vbf算法
* 实现vectorbasedforward\_hop\_by_hop ,hh\_vbf类
* 另外在dbr文件夹中，实现了dbr路由算法

在underwatersensor/uw_common中
基于MobilNode实现了underwatersensornode类
主要实现了水下节点的诸多物理属性，包括三维坐标，移动速度等
基于Agent实现了UWSinkAgent类
作为应用层，实现数据统计，触发发包等功能

基本结构，从底层到上层应该是：

物理层采用underwaterphy和underwaterpropagation，underwaterChannelClass等物理模型MAC层可自选算法
Routing层可自选算法
应用层挂接UWSinkAgent类

所有自编写Agent都要实现command，recv等函数

### VBF算法的实现 ###

接上节叙述，VBF物理层采用三个基本模型，脚本实现如下
{% highlight C++%}
set opt(chan)		Channel/UnderwaterChannel
set opt(prop)		Propagation/UnderwaterPropagation
set opt(netif)		Phy/UnderwaterPhy
set opt(mac)		Mac/UnderwaterMac/BroadcastMac
set opt(ifq)		Queue/DropTail/PriQueue
set opt(ll)		LL
set opt(energy)         EnergyModel
set opt(txpower)        2.0
set opt(rxpower)        0.75
set opt(initialenergy)  10000
set opt(idlepower)      0.008
set opt(ant)            Antenna/OmniAntenna
set opt(filters)        GradientFilter    ;# options

...
# ==================================================================

LL set mindelay_		50us
LL set delay_			25us
LL set bandwidth_		0	;# not used

Queue/DropTail/PriQueue set Prefer_Routing_Protocols    1

# unity gain, omni-directional antennas
# set up the antennas to be centered in the node and 1.5 meters above it
Antenna/OmniAntenna set X_ 0
Antenna/OmniAntenna set Y_ 0
#Antenna/OmniAntenna set Z_ 1.5
Antenna/OmniAntenna set Z_ 0.05
Antenna/OmniAntenna set Gt_ 1.0
Antenna/OmniAntenna set Gr_ 1.0

Agent/Vectorbasedforward set hop_by_hop_ 0

Mac/UnderwaterMac set bit_rate_  1.0e4 ;#10kbps
Mac/UnderwaterMac set encoding_efficiency_ 1
Mac/UnderwaterMac/BroadcastMac set packetheader_size_ 0 ;# #of bytes

# Initialize the SharedMedia interface with parameters to make
# it work like the 914MHz Lucent WaveLAN DSSS radio interface
Phy/UnderwaterPhy set CPThresh_  10  ;#10.0
Phy/UnderwaterPhy set CSThresh_  0    ;#1.559e-11
Phy/UnderwaterPhy set RXThresh_  0    ;#3.652e-10
#Phy/WirelessPhy set Rb_ 2*1e6
Phy/UnderwaterPhy set Pt_  0.2818
Phy/UnderwaterPhy set freq_  25  ;# 25khz  
Phy/UnderwaterPhy set K_ 2.0    ;# spherical spreading
{% endhighlight %}

MAC层选择了BroadcastMac广播MAC
路由层当然挂接VBF路由

VBF算法的具体实现，在vectorbasedforard.cc中，算法的实现
在
{% highlight C++ %}
void VectorbasedforwardAgent::recv(Packet* packet, Handler*);
{% endhighlight %}
中，具体算法流程与论文中的叙述基本一致。

根据算法层层延迟转发，到达Sink，则交给uw_sink应用层agent做相应的统计工作

整体思路大概如此。

但应注意，目前官网提供的aqua-sim，所有uw_sink等都是与vbf算法配套的，包括一些包头的抓取和分析等，都直接默认数据包是vbf数据包。

当修改成dbr算法时，要修改这些配套的内容。具体细节将在下篇博文中总结。

### 代码运行基本流程 ###

最后总结底层代码运行的基本流程

源节点发包

1. 发包由 UWSinkAgent.sendpkt函数周期触发
2. 转到路由层的recv或者send函数，进行数据结构封装
3. 发送给Scheduler调度转发

中继节点转发

1. 路由层Recv函数接到数据包，判断是否重复接收
2. 如需要转发，根据算法模型进行转发处理
3. Set_timer 等待Scheduler调度转发

Sink节点收包

1. 路由层Recv函数接到数据包，判断是否重复接收
2. 首次接受，呈送到UWSinkAgent的Recv函数
3. UWSinkAgent做相应处理，包括计算到达率，总延时，跳数等仿真数据


