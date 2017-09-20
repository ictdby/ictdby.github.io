---
author: bydiao
comments: true
date: 2015-07-05 14:28:14+00:00
layout: post
title: Machine Learning Foundation 7-1
mathjax: true
categories: [Machine Learning]
tags: [MLF]
---

# MLF Chapter 7.1

@(Machine Learning Foundation)

VC dimension

首先明确一点，VC维，是$$\mathcal{H}$$的属性，$$d_{vc}=mbpk-1$$

从B(N,k)出发，来看VC维
B(N,k) 的定义是，某一个k，对于N个输入，最大dichotomies(分类)个数。
分类个数是由shatted决定的
shatter，的定义，在任意k个点不能有$$2^k$$种可能的前提下，$$m_\mathcal{H}(N) = 2^N$$，则称N对于k，可shatter
B(N,k) 是$$m_\mathcal{H}(N)$$ 的上限。

![Alt text](http://pic.yupoo.com/bitcsdby/GLb5OdXm/medish.jpg)


因此我们得到 $$m_\mathcal{H}(N) \leq B(N,k) \leq N^{k-1}$$
我们可以将VC Bound进一步放缩一下，得到

$$P[\exists h \in \mathcal{H} \quad  s.t. | E_{in}(h) - E_{out}(h) | > \epsilon] \\ \leq 4m_\mathcal{H}(2N)exp(-\frac{1}{8} \epsilon^2 N)\\\leq 4(2N)^{k-1}exp(-\frac{1}{8}\epsilon^2N)$$ 

从VC Bound我们可以得到
1. 如果$$m_\mathcal{H}(N)$$ 有break point k，那么这就是一个good的 $$\mathcal{H}$$ Set
2. 如果N足够大，$$E_{out}\approx E{in}$$ 的概率更大
3. 如果$$\mathcal{A}$$可以得到一个更小的 $$E_{in}$$，学习性能会更好

从VC Bound的角度，机器学习的基础理论更加扎实。

下面给出VC Dimension的定义，
VC dimension of $$\mathcal{H}$$, denoted $$d_{vc}(\mathcal{H})$$ is largest N for which $$m_\mathcal{H}(N)=2^N$$ 
等价于 the most input $$\mathcal{H}$$ that can shatter
等价于$$d_{vc}=mbpk - 1$$

两个结论
$$N \leq d_{vc} \rightarrow \mathcal{H} can shatter some N inputs$$
$$if N \leq 2, d_{vc}\leq 2, m_\mathcal{H}(N) \leq N^{d_{vc}}$$

第一小节的最后，我们得到一个最终的结论
有限的$$d_{vc}$$可以保证$$g$$能够满足，$$E_{out}(g) \approx E_{in}(g)$$ 

课程中也给出，该结论与算法$$\mathcal{A}$$，输入的分布$$P$$和目标函数$$f$$ 都不相关。

第一小节的Fun Time，题目确实有些难理解，受到第六章一些图解的干扰，看了论坛大家的讨论，也有一些人产生和我一样的问题。其实我们对知识的理解是对的，但对问题的理解不对，题中所说的 a set of N inputs 不能被$$\mathcal{H}$$ shatter，意思是这N个数据是确定的，如果是2D场景，他们有可能共线，那就无法shatter了，但是这并不能说 $$d_{vc} \geq N$$，因为可能有另外一组N，不共线，就有可能被shatter，那么就有 $$d_{vc} < N$$；反之，如果所有的N的可能，都不能shatter，那一定是$$d_{vc} < N$$，所以这道题选择4，不能从题中判断出任何结论。
 