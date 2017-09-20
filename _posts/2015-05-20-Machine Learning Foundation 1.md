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

# MLF Chapter 1
@(Machine Learning Foundation)
1.  What is ML
	人类肉眼观察，大脑学习，形成Skill
	客观世界数据data，机器学习，形成Skill

	ML: improving some performance measure with experience computed from data.
2.  ML is necessary when 
	* Human can not define a solution: Speech recogenition
	* Human expertise does not exist: Navigation on Mars
	* Rapid decision, Change over time: network routing, high-frequency trading.
	* Massive scale, adapted to particular cases: consumer-targeted marketing.
3.  适用ML解决的问题特征
	* 存在潜在的模式 Pattern，可以通过挖掘Pattern来提升某一方面的效能。
	* 不能通过简单，确定性的程序实现，例如判断奇偶性就是一个简单确定性问题，不需要学习。
	* 有足够丰富的data作为输入
4.  机器学习的构成
Input   $$ x \in X $$                         
Output $$ y \in Y $$
Target  is to find out $$ f: X \rightarrow Y $$ .  But in general，f is unavailable. 
Data: D={($$ x_1,y_1 $$)....($$ x_n,y_n $$)}
Hypothesis:  $$ g: X \rightarrow Y $$ learned formula to fit $$ f:X\rightarrow Y $$
 
















