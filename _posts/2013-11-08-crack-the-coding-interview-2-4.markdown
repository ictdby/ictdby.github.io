---
author: bydiao
comments: true
date: 2013-11-08 08:41:44+00:00
layout: post
slug: crack-the-coding-interview-2-4
title: 'Crack the Coding Interview: 2.4'
wordpress_id: 547
categories:
- 面试题
tags: [面试题]
---

2.4
You have two numbers represented by a linked list, where each node contains a single digit. The digits are stored in reverse order, such that the 1’s digit is at the head of the list. Write a function that adds the two numbers and returns the sum as a linked list.

EXAMPLE

Input: (3 –> 1 –> 5), (5 –> 9 –> 2)

Output: 8 –> 0 –> 8

两个数字是由链表表示的，head是个位，求这两个链表数字的和。

该题要考虑一个位数多，一个位数少的问题，还有进位的问题，其他的没什么难度。

下面实现的代码是输出一个数字，而不是输出一个链表。

	int add(Node* h1,Node* h2)
	{
		long rlt = 0;
		int dig = 0;
		Node* p1 = h1;
		Node* p2 = h2;
		int c = 0;
	
		while(p1 != NULL || p2 != NULL)
		{
			if(p1 == NULL)
			{ 
				rlt += (p2->data + c) *  	pow(10.0,double(dig));
				p2 = p2->next;
				c = 0;
			}
			else if(p2 == NULL)
			{ 
				rlt += (p1->data + c) *  pow(10.0,double(dig));
				p1 = p1->next;
				c = 0;
			}
			else	
			{
				int local_rlt = p1->data + 	p2->data;
				p1 = p1->next;
				p2 = p2->next;
				rlt += (local_rlt % 10 + c) * pow(10.0,double(dig));
				c = local_rlt / 10;
			}

			dig ++;
		}

		return rlt;
	}
