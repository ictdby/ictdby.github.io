---
author: bydiao
comments: true
date: 2013-10-23 06:21:46+00:00
layout: post
slug: craking-the-coding-interview%ef%bc%9a1-3
title: Craking the Coding Interview：1-3
wordpress_id: 469
categories: [面试题]
tags: [面试题]
---

craking the coding interview 150道题是一本经典的算法教材，自己学习并实现后，将在本博客上逐一总结。

前三题请轻松开场

第一题
Implement an algorithm to determine if a string has all unique characters. What if you can not use additional data structures?
判断一个字符串是否出现重复字符，该题运用位图的思路，
可优化的地方是位图的数据结构，和面试官交流的地方是确定字符集的范围，这样可以优化位图结构
代码如下：
以所有ascii码为字符集的情况

[code lang="cpp"]
bool unique_char(char* a)
{
	char tmp[32] = {0};
	int l = strlen(a);

	for(int i = 0;i < l;i++) 	{ 		if((tmp[a[i] / 8] >> (a[i] % 8)) == 1)
			return false;
		else
			tmp[a[i] / 8] |= (1 << (a[i] % 8));
	}

	return true;
}
[/code]

第二题
Write code to reverse a C-Style String. (C-String means that “abcd” is represented as five characters, including the null character.)

反转字符串，很简单，代码如下：

[code lang="cpp"]
void reverse(char* str)
{
	char* s = str,*e = str+strlen(str)-1;

	while(s < e)
	{
		*s = *s ^ *e;
		*e = *s ^ *e;
		*s = *s ^ *e;

		s++;
		e--;
	}
}
[/code]

第三题
Design an algorithm and write code to remove the duplicate characters in a string without using any additional buffer. NOTE: One or two additional variables are fine. An extra copy of the array is not.
FOLLOW UP
Write the test cases for this method.
这题与第一题类似，可以用位图法，唯一区别是要用去重，可以和面试官交流用某种字符去重。
测试用例，要考虑空字符串，重复字符串，非重复字符串，联系重复字符串，非联系重复字符串等等。
代码如下：

[code lang="cpp"]
char* check_duplicated(char* str)
{
	char tmp[32] = {'\0'};

	int l = strlen(str);

	for(int i = 0;i < l;i++) 	{ 		if((tmp[str[i] / 8] >> (str[i] % 8)) == 1)
			str[i] = ' ';
		else
			tmp[str[i] / 8] |= (1 << str[i] % 8);
	}

	return str;
}
[/code]

编此题的时候，暴露出一个基础知识问题如下：

当定义
[code lang="cpp"]
char* a = "diaoboyu";
check_duplicated(diaoboyu);
[/code]
会报错，"写入位置 0x009da945 时发生访问冲突"
而定义如下
[code lang="cpp"]
char a[] = "diaoboyu";
check_duplicated(diaoboyu);
[/code]
的时候则正常。

原因是，
char* a = "abcd" 这样的定义，编译器会将a作为一个字符串常量，
char a[]="abcd"，那么这里相当于是用“abcd”这个字符串常量，初始化了一个字符串变量a，a则是一个字符串局部变量，可以修改赋值。
简单的说 char* a = "abcd"，程序只分配了指针的内存，指向常量“abcd”，不可修改；而char a[]=“abcd”，则分配了内存，存储了“abcd”的一个副本，可以修改。
这个C++的基础知识，显然比这道题的意义要大。
