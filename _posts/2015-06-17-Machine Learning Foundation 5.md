---
author: bydiao
comments: true
date: 2015-06-17 14:28:14+00:00
layout: post
title: Machine Learning Foundation 5
mathjax: true
categories: [Machine Learning]
tags: [MLF]
---

# MLF Chapter 5

@(Machine Learning Foundation)

本章的主题是Test Vs Training，但并直接讨论欠拟合和过拟合的的问题，而是从$$E_{out}(g)$$和$$E_{in}(g)$$出发，讨论过拟合和欠拟合的本质。

问题是这样提出的

![Alt text](../image/MLF5_1.PNG)

一个机器学习的过程如上图所示，我们有一系列的数据，有一个假设集合，每个假设都对应相应的算法。算法的输入是假设和数据，输出则是一个函数$$g$$。一个问题可学习是基于一个同分布假设的，也就是全量数据与样本数据有近似的分布，等价于$$g \approx f$$。我们不能得到全量数据的f和分布P，我们只能通过样本数据去学习到$$g$$。

对于任意一个学习问题，我们有两个目标

$$E_{out}(g) \approx E_{in}(g)$$
$$E_{in}(g) \approx 0$$

前者是要让test偏差尽量小，后者则是让train误差尽量小。二者是trade-off的关系。

进一步引申这个trade-off，我们可以发现用M来解释，M是假设集合的模。

|target|small M| large M|
|---|---|---|
|$$E_{out}(g) \approx E_{in}(g)$$|Yes $$P[Bad] \leq 2Mexp(...)$$ is small| No P[BAD] is large|
|$$E_{in}(g) \approx 0$$|No two few choices|Yes many choices|

似乎解释了过拟合的本质。

以上就是本章的理论和心，后三节则主要在讨论在M无限的时候，例如PLA，如何保证P[BAD]的上界也是有限的一个值。

首先提出了一个定理，
**定理1：** 一个2D平面，将输入的N个点分为两类，最多有效直线的个数是$$2^N$$

提出了一个概念，Growth Function，增长函数，定义了M关于输入集合大小N的函数，

对于2D平面的二分类问题，$$M \leq 2^N$$

这里已经给出了一个M的上界，PLA无限的问题已经可以得到解释。

最后一节，又提出了一个概念，最小分割点(minimum break point)，满足$$M(k) < 2^k$$的最小的k，例如在2D PLA中，k=4时，M=14而不是16，因此 minimum break point of PLA就等于4。

那么就有定理2

**定理2：**如果存在 minimum break point k，则$$m_h(k) = O(N^{k-1})$$，这样就有进一步缩小了M的上界。

本章主要从M的角度出发，讨论了机器学习两个目标，test偏差和train误差。提出了可以用$$m_h{N}$$来替代无限大的$$M$$，具体证明将在接下来的内容中讲解。 