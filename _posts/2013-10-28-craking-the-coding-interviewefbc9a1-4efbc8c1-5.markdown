---
author: bydiao
comments: true
date: 2013-10-28 09:23:22+00:00
layout: post
slug: craking-the-coding-interview%ef%bc%9a1-4%ef%bc%8c1-5
title: Craking the Coding Interview：1.4，1.5
wordpress_id: 490
categories: [面试题]
tags: [面试题]
---

1.4
Write a method to decide if two strings are anagrams or not

该题同样运用位图的思想，两个字符串拥有同样的位图，那就是 anagrams。
具体实现如下：

	bool is_anagrams(char* a,char* b)
	{
		char bit_a[256] = {'\0'};
		char bit_b[256] = {'\0'};
		int l_a = strlen(a);
		int l_b = strlen(b);
	
		for(int i = 0;i < l_a;i++)
			bit_a[a[i]] ++;
		for(int i = 0;i < l_b;i++)
			bit_b[b[i]] ++;
	
		for(int i = 0;i < 256;i++)
			if(bit_a[i] != bit_b[i])
				return false;

		return true;
	}	


1.5
Write a method to replace all spaces in a string with ‘%20’.
该题是一个字符串延长的问题，如果发现一次空格就插入一次的话，复杂度为n方，如果将字符串复制到另一个字符串上，并实现计算好新字符串的长度，复杂度就是n，代码如下


	char* replace(char* a)
	{
		int l_a = strlen(a);
		int n = 0;
	
		for(int i = 0;i < l_a;i++)
			if(a[i] == ' ')
				n++;
	
		char* b = new char[l_a + n*2];
	
		memset(b,0,strlen(b));
		for(int i = 0,j=0;i < l_a;i++)
		{
			if(a[i] != ' ')
				b[j++] = a[i];
			else
			{
				b[j++] = '%';
				b[j++] = '2';
				b[j++] = '0';
			}
		}
	
		return b;
	}


要注意的是 new的变量在堆中，可以在函数中通过指针返回，栈中的局部变量不能返回，返回的是一个无效的值。
