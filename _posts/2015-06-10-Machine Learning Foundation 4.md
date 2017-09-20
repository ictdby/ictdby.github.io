---
author: bydiao
comments: true
date: 2015-06-10 14:28:14+00:00
layout: post
title: Machine Learning Foundation 4
mathjax: true
categories: [Machine Learning]
tags: [MLF]
---

# MLF Chapter 4

@(Machine Learning Foundation)

第四章主要讨论了什么是可学习的问题，以及机器学习的一个重要的理论基础，可以回答为什么可以通过样本数据来学习全部输入空间的数据这个问题。


1. Learning is impossible
这一小节主要是论证了，除非给你确定性的if else条件，否则通过样本，完全确定的学习输入空间的$$f$$，是不可能的。给了一系列的实例，

2. Inferring Something Unknown
这一小节提出了一个数学问题，假设一个大大的盒子里有红绿两种颜色的球，个数非常多无法数过来，红色的概率是$$\mu$$，现在我们要估计出这个概率，于是就从盒子里取球，取了$$N$$个，得到红色的概率是$$\nu$$，那么Hoeffding's inequality给出了一个误差的上界
$$P(|\mu - \nu| > \varepsilon) \leq 2exp(-2\varepsilon^2N)$$
这个不等式可以从两个方面去理解
* 采样N变大后，$$P(|\mu-\nu| > \varepsilon)$$的概率上界会越来越小，因此$$\mu$$，$$\nu$$越来约接近
* $$\mu$$，$$\nu$$的差$$\varepsilon$$取值很大的时候，即相差很大的时候，上界的概率也会很小。
简单的说，取样大的概率上界小，相差大的概率上界小。因此我们说 $$\mu=\nu$$很可能正确，probably approximately correct（PAC）
这也就让从已知推测为止成为可能，也是机器学习一条基本的理论基础。
3. Connection to Learning
第三小节主要将机器学习问题，形式化为霍夫丁不等似的表达形式。

	|项目|红绿球|learning|
	|---|---|---|
	|问题|确定红球概率$$\mu$$|确定h(x)相对于f(x)正确的概率|
	|输入|球|x|
	||红球|h 不正确 h(x) != f(x)|
	||绿球|h 正确 h(x) == f(x)|
	|样本数量|N|D的数量n|
这样，$$\mu$$和$$\nu$$ 则对应了机器学习中的 $$E_{out}(h)$$，out-of-sample-error期望和$$E_{in}(h)$$，in-sample-error期望。
$$P(|E_{out}(h) - E_{in}(h)| > \varepsilon) \leq 2exp(-2\varepsilon^2N)$$
因此我们可以说，$$E_{out}(h) =E_{in}(h)$$  PAC
进一步说，机器学习的目标，就是学习出一个$$g$$，使得输入数据的$$E_{in}(h)$$尽量小。
4.Connection to Real Learning
这小节主要在论证，h的选择对最后结果的影响，如果h的判断全是对的，或者全是错的，或者呈某一种分布，对真实情况的f而言，可能都有其不足之处。
但只要h的选择是有限个的，3小节中的概率上界公式就是收敛的，只不是多了一个系数而已。
在h有无限多个的情况下，仍然成立，但证明会在接下来的课程中介绍。
个人感觉，第四章的内容有些暗含过拟合，欠拟合的意思。
这一章确实是机器学习的基石，之前并没有看到过类似的讲解，听过之后，很受启发。有时间应该看一下霍夫丁不等式的原文。  
