---
author: bydiao
comments: true
date: 2015-05-25 14:28:14+00:00
layout: post
title: Machine Learning Foundation 2
categories: [Machine Learning]
mathjax: true
tags: [MLF]
---

# MLF chapter 2
@(Machine Learning Foundation)
感知机模型来解决Yes No问题

1. 假设 $$x\in R^2$$

$$ h(x) = sign(\Sigma^N_{i=1}\omega_ix_i - threshold) $$

为学习threshold，加入$$ x_0=1 $$ $$\omega_0=-threadhold $$
则有 $$ h(x)=sign(\Sigma^N_{i=0}\omega_ix_i) $$
目标是学习出 $$ \omega^T $$，使得所有的$$ sign(\omega^Tx_i) = y_i $$
进而得到 $$ g=sign(\omega^Tx_i) $$，用于其他数据预测。

2.  Perceptron Learning Algorithm
 For t = 0,1,...
	* find a mistake $$ w_t $$ called $$ (x_i,y_i) $$    $$ sign(\omega_t^Tx_i) \neq y_i $$
	* correct mistake by $$ \omega_{t+1}\leftarrow \omega_t+y_ix_i $$
	* until all $$ x \in D $$ correct on $$ w $$
	* return $$ \omega $$ as g

3.  下图从几何上说明了PLA Correct的实质。
	$$ cos\theta = \frac{\omega x}{|\omega||x|} $$
	因此$sign(\omega x)$的实质，就是从原点到x点的向量，与法向量$$ \omega $$之间的夹角是在[$$ -\frac{\Pi}{2} $$,$$ \frac{\Pi}{2} $$]区间，还是在[$$ \frac{\Pi}{2}$$,$$\frac{3\Pi}{2}$$]区间。如果是前者，正确情况应该是对应+1，后者则对应-1。如果出现错误，则是+1的情况出现了[$$ \frac{\Pi}{2}$$,$$\frac{3\Pi}{2}$$区间的夹角，则需要将夹角拉回到[-$$-\frac{\Pi}{2}$$,$$\frac{\Pi}{2}$$]，或者是-1的情况出现了[$$-\frac{\Pi}{2}$$,$$\frac{\Pi}{2}]$$夹角，需要拉回到[$$\frac{\Pi}{2}$$,$$\frac{3\Pi}{2}]$$。如下图所示。
![Alt text](./MLF2_1.png)

4.  PLA收敛性证明
假设$$x\in D$$ 中的所有点线性可分，则存在一条直线，法向量为$$\omega_f^T$$
由PLA方法可知，当遇到错误的时候，有如下公式进行修正

$$\omega_{t+1} \leftarrow \omega_t + y_nx_n$$

则有

$$\omega_{f}\omega_{t+1} = \omega_f\omega_t + y_n\omega_fx_n$$

由题目可知，存在距离分割线最近的点$(x_n^i,y_n^i)$
则有

$$y_n\omega_fx_n \geq y_n^i\omega_fx_n^i > 0$$

$$\omega_{f}\omega_{t+1} > \omega_f\omega_t                    \qquad   (1)$$

从几何上可知，两条向量的方向向着平行的方向变化。
另有，PLA在出现错误的时候进行修正即修正时

$$y_i\omega x_i < 0$$

则有

$$||\omega_{t+1}||^2 = (\omega_t + y_ix_i)^2 \\ =||\omega_t||^2+2\omega_tx_iy_i+x_i^2 < ||\omega_t||^2 + x_{max}^2$$

整理后得到

$$||\omega_{t+1}||^2 < ||\omega_t||^2 + ||x_{max}||^2 \qquad (2)$$

设$$\omega_0 = 0$$，PLA运行T次，可以收敛，由(1)(2)可得到

$$T \leq \frac{||x_{max}||^2}{(y_{min}\frac{w_f^T}{||w_f^T||}x_{min})^2}$$

存在上限，则PLA算法可收敛，证明完毕。

5.  非线性可分的情况
当数据集非线性可分的情况，PLA将无休止运行下去。
这时，可以确定一个假设

$$w_g \leftarrow argmin_\omega\Sigma^N_{n=1}[y_n \neq sign(\omega^Tx_n)]$$

得到一个损失最小的$\omega$
设置迭代次数，最终得到结果
该方法要比PLA慢，可分析，PLA是$$O(n)$$，而该方法是$$O(n^2)$$



第二章，最重要的是学会用几何向量方法来分析模型，证明PLA收敛性。 
