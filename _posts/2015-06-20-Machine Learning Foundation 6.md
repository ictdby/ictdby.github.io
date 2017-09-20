---
author: bydiao
comments: true
date: 2015-05-20 14:28:14+00:00
layout: post
title: Machine Learning Foundation 1
mathjax: true
categories: [Machine Learning]
tags: [MLF]
---

# MLF Chapter6

@(Machine Learning Foundation)

Theory of Generalization，泛化理论

所谓泛化，就是将$$g$$用在 out-of-sample的数据上。
泛化能力，就是$$g$$在out-of-sample上的准确性。

本章的前三节，还是在继续上一张，围绕感知机可学习性的证明。

第一节，主要在形象的讨论，输入N与break point K的关系。
从上一章我们已经知道，
$$m_h(N) < 2^N$$
本节的内容是为后面做铺垫，最终目的是想证明
$$m_h(N) \leq poly(N)$$

此处再明确一下shatter的概念，shatter k，就是任意k个输入，不能存在$$2^k$$种组合

第二节，主要提出了一个函数，$$B(N,k)$$，最大可能组合N和break point k。

本节主要是证明 $$B(N,k) \leq poly(N)$$

第三节，证明了
$$B(N,k) \leq \Sigma_{i=0}^{k-1}C(N,i)$$

简单整理一下一些概念

1. 假设集合大小 $$|M|$$
2. 有效假设集合大小 $$effective(N)$$
3. 最小分割点 break point k
4. 成长函数 Growth Function，$$m_h(N)$$
5. 成长函数的边界函数 $$B(N,k)$$

目前我们得到的结论是
$$m_h(N) \leq 2^N$$
$$B(N,k) \leq \Sigma_{i=0}^{k-1}C(N,i)$$

从以上两个式子可知，成长函数的边界函数是N的多项式，那么成长函数也是N的多项式，如果break point存在的话。

到目前，我们证得
$$m_h(N) \leq O(N^{k-1})$$

第四节，则向最初的2D感知机可学习问题发起总攻，利用以上的结论进行最后的证明。

最终证明了 Vapnik-Chervonenkis (VC) bound 形式如下

$$P[\exists h \in \mathcal{H} \quad  s.t. | E_{in}(h) - E_{out}(h) | > \epsilon] \leq 4m_h(2N)exp(-\frac{1}{8} \epsilon^2 N)$$ 

这样，2D感知机的上界就找到了，也就证明了他是可学习的。 