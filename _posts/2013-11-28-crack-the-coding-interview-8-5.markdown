---
author: bydiao
comments: true
date: 2013-11-28 09:36:12+00:00
layout: post
slug: crack-the-coding-interview-8-5
title: 'Crack the coding interview: 8-5'
wordpress_id: 584
categories:
- 面试题
tags: [面试题]
---

Implement an algorithm to print all valid (e.g., properly opened and closed) combinations of n-pairs of parentheses.

EXAMPLE:

input: 3 (e.g., 3 pairs of parentheses)

output: ((())), (()()), (())(), ()(()), ()()()


输出n对括号所有合法的组合

这道题的递归方法和上面一道题很像，也可以将递归理解成所有解集的一棵树，遍历这棵树，并分支限界，找到合法的解输出即可。

这道题递归参数设计，就是左括号个数和有括号个数，以及当前的组合方式的字符串。

从 1 0 开始，每层递归l+1 r和 l r+1，并判断不超过n

递归终止条件是l==r==n,则这是找到一个合法的解，输出即可，r>l,这时一定是一个不合法的解，直接返回即可。

递归的实现代码如下：

{% highlight c++ %}
void match(int l,int r,int n,char s[])
{
	if(r > l)
		return ;
	if(l == n && r == n)
	{
		cout << s << endl;
		return ;
	}
		
	if(l < n)
	{
		s[r+l] = '(';
		match(l+1,r,n,s);
	}
	if(r < n)
	{
		s[r+l] = ')';
		match(l,r+1,n,s);
	}
}
{% endhighlight %}

还是两点，参数设计和返回边界条件。

最近对一类递归问题的体会是，递归就是一棵树，用递归把所有可能的解枚举出来，分支限界，最终找到需要的解。

斐波纳挈数列是另一类问题，相当于不断迭代，从上到下，迭代到最底层再反向迭代，最终得到一个解。

两类的递归设计思路有一些区别。
