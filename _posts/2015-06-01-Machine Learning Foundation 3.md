---
author: bydiao
comments: true
date: 2015-06-01 14:28:14+00:00
layout: post
title: Machine Learning Foundation 3
mathjax: true
categories: [Machine Learning]
tags: [MLF]
---

# MLF Chapter 3

@(Machine Learning Foundation)
### Type of Learning

本章对从四个角度对机器学习进行了分类，分别是
###### 不同的输出空间
###### 不同的Label
###### 不同的学习流程
###### 不同的输入空间

看过这章之后，对机器学习知识体系有了更深刻的了解。下面详细总结一下


1. 不同输出空间
机器学习的输出，也就是学习的结果，机器学习的核心是通过现有数据，探索最适合的学习模型，得到一个最合适的函数$$g$$，以此对新得到的样本$x$$进行预测，预测的结果可能是一个分类，也可能是一个值，也可能是一个描述性的结构。这就产生了四种不同的输出空间，对应四类机器学习的问题。

	|类别|描述|
	|---|---|
	| binary classification | 0-1 二分类问题|
	|multiclass classification|	0，1，2，3，4，多分类问题|
	|regression	|回归问题，连续或者离散的一系列结果，可能是无限的|
	|structured learning|结构学习，NLP，学习一个句子的结构，可能被描述为一个串，如PVN，PVP，NVN等|
2. 不同的label
机器学习的输入是$$D:x_1,x_2,x_3...$$ 还是 $$D:(x_1,y_1),(x_2,y_2),(x_3,y_3)$$，可以将机器学习分为四类。

	|类别|描述|
	|---|---|
	|supervised 监督学习|y_n|
	|unsupervised 非监督学习|no y_n|
	|semi-supervised 半监督学习|some y_n, not all|
	|reinforcement 强化学习|让机器对y_n的理解越来越深刻|
3. 不同的学习流程
学习的不同流程和实际问题的需求紧密相关，主要分为离线批处理学习，在线学习和主动学习

	|类别|描述|
	|---|---|
	|batch|离线批处理|
	|online|在线学习，通过在线输入的数据，不断更新模型参数|
	|active|模型可以主动提问|
4. 不同的输入
输入对于一个机器学习问题来说尤为重要，同一组数据，变换不同的输入空间，对学习的结论有很大影响。
* 有一些情况，机器学习的输入可能是很确定的，比如房价预测，给了两列数据，（面积，构建时间），那这两列数据就是很明确的输入信息，这称为concrete feature
* 一些情况，机器学习的数据虽然不确定，但是能直接从输入数据的原始属性中抽象出来，比如一副16*16的图片，有256个像素点，那么将这256个像素点的灰度值作为一个向量来表示这个输入，就是对图片的原始属性进行了抽象，这叫做raw feature
* 还有一些情况，输入没有任何物理含义可以进行抽象，需要从数据出发，抽象出一系列的feature，来表示这个输入，例如广告ID，用户ID等

Feature的抽象是一个机器学习问题的关键。
|类别|描述|
|---|---|
|concrete feature|确定的特征|
|raw feature|从物理属性中抽象出来的特征|
|abstract feature|完全抽象自输入的特征，与物理属性无关| 