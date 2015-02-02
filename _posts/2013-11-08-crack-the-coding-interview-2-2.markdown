---
author: bydiao
comments: true
date: 2013-11-08 08:17:27+00:00
layout: post
slug: crack-the-coding-interview-2-2
title: 'Crack The Coding Interview : 2.3'
wordpress_id: 543
categories:
- 面试题
tags: [面试题]
---

2.2
Implement an algorithm to delete a node in the middle of a single linked list, given only access to that node.

EXAMPLE

Input: the node ‘c’ from the linked list a->b->c->d->e Result: nothing is returned, but the new linked list looks like a->b->d->e

只给出指向节点的指针，删除一个单链表中的节点

此题想法很简单，删除该节点，我们可以转移成删除下一个节点，并把下一个节点的数据域复制到当前节点上，这样就可以实现单链表的节点删除。

需要考虑的是，指针指向的节点是头节点，中间某节点，尾节点，还是空指针。

前两种情况正常处理。如果是尾节点，单纯delete该指针并不能起到作用，因为其前端节点的next并不是空，好的方法是将该节点的数据域赋值为一个特殊值，发现后不输出即可。如果是空指针，直接返回错误即可。

实现代码如下：


	#include <iostream>
	#include <string>
	using namespace std;
	
	typedef struct node
	{
		int data;
		struct node* next;
	}Node;
	
	bool remove(Node* c)
	{
		if(c == NULL )
			return false;
		if(c->next == NULL)
		{
			delete c;
			return true;
		}
	
		Node* p = c->next;
	
		c->data = p->data;
		c->next = p->next;
		
		delete p;
		return true;
	}

	int main()
	{
		int n = 10;
		Node* head = new Node();
		head->next = NULL;
		Node* p = NULL;
		p = head;
	
		for(int i = 0;i < n;i++)
		{
			p->data = i;
	
			if(i != n-1)
			{
				p->next = new Node();
				p = p->next;
				p->next = NULL;
			}
			else
				p->next = NULL;
		}
	
		p = head;
	
		for(int i = 0;i < 4;i++)
			p = p->next;
	
		remove(p);
		
	
	}
