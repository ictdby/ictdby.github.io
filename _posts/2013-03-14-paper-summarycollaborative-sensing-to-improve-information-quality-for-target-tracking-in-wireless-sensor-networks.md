---
layout: post
title: Collaborative Sensing to Improve Information Quality for Target
  Tracking in Wireless Sensor Networks
categories: [Wireless Sensor Network]
tags: [Wireless Sensor Network]
---

Authors:Wendong Xiao and Chen Khon Tham  Sajal K.Das
From:PerCom2010
Key word:information quality;wireless sensor networks;target tracking;joint sensing;sensor scheduling;collaborative sensing;kalman filter
Cition:2

这篇论文短小精悍，思想独到。

全篇论文的主题是通过collaborative sensing来提高information quality。其中最独特的地方是sensing级别的collaboration，本文主要以超声波为例，说明传感器协同的基本概念。
Abstract

提出可以通过emitting sensor实现传感器的sensing协同，通过扩展卡尔曼滤波实现对物体的状态估测，通过蒙特卡洛方法实现监测概率的计算。
Introduction

提出对Information quality的重视越来越高。提到一个重要观点：传感器可分为主动传感器如超声波等emitting sensor以及温湿度，压力等被动传感器主动传感器可以用于本文提到的Joint sensing
Joint Sensing

假设所有传感器是同步的，同种的；为避免超生干扰，同一时间假设只有一个节点发出超声波。这样就是一个发，多个接，每个接到超声波的节点域发送节点都满足一个方程：
$$d(s,t)+d(s_i,t) = v\Delta t$$
其中v为超生速度，$$\Delta t$$为发信号到收到信号的时间。$s_i$代表接受节点,$s$代表发节点。

基于这点事实，就可以通过EKF判断目标的位置，并量化IQ。EKF具体实现没有细看。
同时为实现精确调度各个节点，以实现最低功耗跟踪目标，需要计算下一时刻每一节点的监测概率。用到蒙特卡洛算法。具体待细看。
Sim
仿真结果显示，改方法可以保证大部分时间内（90%）实现多节点的传感协同。
但本文的方法仅适用于封闭的小区域，而且没能很好的解决emitting sensor的角度问题，不适合动作复杂的目标。
Idea
本算法非常适用于智能家居，室内监控的等场景。另外，超声波放出的波形应该不是一个平面纺锤形，可以考虑三维场景下的应用。无论两维还是三维，都满足上述的几何公式。
卡尔曼滤波，蒙特卡洛这些东西是不可逾越的数学基础，应该专心研究一下。
