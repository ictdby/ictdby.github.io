---
author: bydiao
comments: true
date: 2015-07-12 14:28:14+00:00
layout: post
title: Machine Learning Foundation 7-2-3-4
mathjax: true
categories: [Machine Learning]
tags: [MLF]
---

# MLF Chapter 7.2 3 4
@(Machine Learning Foundation)

$$d_{vc}$$的多维度推广

结论：d 维度的输入，$$d_{vc} = d + 1$$

$$d_{vc}$$ 的物理含义，表征了假设$$\mathcal{H}$$的能力，$$d_{vc}$$越大，越强。

再加上7.1中的结论

$$P[\exists h \in \mathcal{H} \quad  s.t. | E_{in}(h) - E_{out}(h) | > \epsilon] \\ \leq 4m_\mathcal{H}(2N)exp(-\frac{1}{8} \epsilon^2 N)\\\leq 4(2N)^{d_{vc}}exp(-\frac{1}{8}\epsilon^2N)$$ 

我们就发现一个trade-off

|目标|$$d_{vc}$$ 大|$$d_{vc}$$ 小|
|---|---|---|
|$$E_{in}(g) \approx E_{out}(g)$$|P[BAD] 大，不利|P[BAD] 小，有利|
|$$E_{in}(g) \approx 0$$|$$\mathcal{H}$$ 强，有利|$$\mathcal{H}$$ 弱，不利|


以上是7.2 7.3的主要内容。

7.4 节则主要从数学上对$$d_{vc}$$ 进行解释

领
$$\delta = 4(2N)^{d_{vc}}exp(-\frac{1}{8}\epsilon ^2 N)$$

则有
$$E_{out}(g) \leq E_{in}(g) + \sqrt{\frac{8}{N} ln(\frac{4(2N)^{d_{vc}}}{\delta})}$$

![Alt text](http://pic.yupoo.com/bitcsdby/GLb3UpEn/medish.jpg)

从这个角度出发，我们可以得到以上的曲线，从数学上解释了$$d_{vc}$$的trade-off

但这仅仅是理论上的解释，并不够practical

如果我们从理论出发，很多问题是还是无法解决的![Alt text](http://pic.yupoo.com/bitcsdby/GLb3UEvp/medish.jpg)


如图所示，要满足既定的误差上线，我们需要3万个点来做学习，拿到30000个点是不太可能的。
不过按照经验来说，更practical的方法，是拿到10倍 $$d_{vc}$$的N即可进行学习。

本章主要介绍了VC 维的概念，这是假设集 $$\mathcal{H}$$的重要属性，表征假设的学习能力。

1. 有限的$$d_{vc}$$保证了 $$E_{out}(g) \approx E_{in}(g)$$
2. d维输入，$$d_{vc} = d + 1$$
3. $$d_{vc}$$ 越大可以保证，$$E_{in} \approx 0$$
4. $$d_{vc}$$，可以从数学上解释两个学习目标之间的trade-off
5. $$d_{vc}$$，可以从理论上确定输入集合与误差上限之间的关系


 