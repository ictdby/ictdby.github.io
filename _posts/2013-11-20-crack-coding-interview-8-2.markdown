---
author: bydiao
comments: true
date: 2013-11-20 09:20:20+00:00
layout: post
slug: crack-coding-interview-8-2
title: 'Crack Coding Interview: 8-1'
wordpress_id: 551
categories:
- 面试题
tags: [面试题]
---

Write a method to generate the nth Fibonacci number.

求第n个斐波纳挈数


	int fn(int n)
	{
		if(n < 1)
			return -1;
		if(n == 1 )
			return 1;
		if(n == 2)
			return 1;
	
		return fn(n-1)+fn(n-2);
	}


最通用的算法是递归，这样可以在O(n)的时间复杂度实现该算法

另可通过快速求整数幂的方法，以O(logn)的时间复杂度实现。

这里涉及到两个点，一个是斐波纳挈的递推公式，如下图所示

一个是求一个数的幂指数算法

x^5 = x^4 * x^1

因此，我们只需得到x^1到x^logx次方，就可以求出x^n，复杂度为logn

具体算法如下

	int pow(int x,int y)
	{
		int rlt = 1;
		int m = x;
		while(y > 0)
		{
			if(y & 1)
				rlt *= m;
			
			m *= m;
	
			y >>= 1;
		}
	
		return rlt;
	}

这样，求斐波那契数转化为求矩阵幂运算，幂运算又可以用快速算法解决，整体复杂度降为O(logn)
只需要将整数乘法变为矩阵乘法即可。

求第n个斐波纳挈数，可递归，可递推
