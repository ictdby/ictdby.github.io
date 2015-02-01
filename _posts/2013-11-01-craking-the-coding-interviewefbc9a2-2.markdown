---
author: bydiao
comments: true
date: 2013-11-01 03:16:22+00:00
layout: post
slug: craking-the-coding-interview%ef%bc%9a2-2
title: Craking the Coding Interview：2.2
wordpress_id: 536
categories:
- 面试题
tags: [面试题] 
---

2.2
Implement an algorithm to find the nth to last element of a singly linked list.

找到单项链表的倒数第n个元素，这是一个很古老的问题了，有两个解决思路

一个是用栈或者递归，O(n)的复杂度可以找到倒数第k个元素，递归实现如下：


	int nth_to_last = 0;
	int rlt = 0;
	void get_nth_last(Node* p)
	{
		if(p == NULL)
			return ;
	
		get_nth_last(p->next);
	
		if(nth_to_last == 1)
		{
			rlt = p->data;
		}
	
		nth_to_last--;
	}

另一种方法是用双指针，一个指针从头移动k个，然后再将一个指针指向头，两个同时移动，直到链表结尾，这样，后放的指针，指向的就是倒数第n个，这样只扫描链表1次，时空效率都比上面的递归要好一些。


	int double_pointer(Node* head,int k)
	{
		Node* p1 = NULL,*p2 = NULL;
		p1 = head;
		p2 = head;
	
		for(int i = 0;i < k;i++)
			p1 = p1->next;
	
		while(p1 != NULL)
		{
			p1 = p1->next;
			p2 = p2->next;
		}
	
		return p2->data;
	
	}
