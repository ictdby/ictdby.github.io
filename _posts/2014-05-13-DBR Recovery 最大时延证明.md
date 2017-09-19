---
layout: post
title: DBR Recovery 最大时延证明
mathjax： true
categories: [WSN]
date: 2014-05-13
tags:
- DBR
- UWSN
---

首先列出两个函数，一个是round trip时延函数，一个是holding time函数

$$f(d) = \frac{2\tau}{\delta}(R-d)+$$
和
$$p(d) = \frac{2d}{\sin\theta \cdot v_0}$$

那么全局的时延 则是

$$t(d) = f(d) + p(d)$$

取$$\delta = R$$
则$$t(d) = 2\tau-\frac{2\tau d}{R} + \frac{2d}{\sin\theta \cdot v_0}$$

d 属于$$(0,R]$$

取d = $$\frac{R}{n}$$,其中n 属于 [1,$$\infty$$)

则 
$$t(n) = 2\tau-\frac{2\tau}{n}+\frac{2\tau}{\sin\theta \cdot n}$$

其中

$$\sin\theta >= \frac{d}{R}$$

则
$$t(n) <= 2\tau - \frac{2\tau}{n} + 2\tau$$

$$\lim\limits_{n \rightarrow \infty}t(n) = 4\tau$$

最终得到
$$2\tau <= t(d) <= 4\tau$$
