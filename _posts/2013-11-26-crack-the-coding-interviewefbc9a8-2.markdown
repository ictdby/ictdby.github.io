---
author: bydiao
comments: true
date: 2013-11-26 08:33:59+00:00
layout: post
slug: crack-the-coding-interview%ef%bc%9a8-2
title: Crack the coding interview：8-2
wordpress_id: 570
categories:
- 面试题
tags: [面试题]
---

Imagine a robot sitting on the upper left hand corner of an NxN grid. The robot can only move in two directions: right and down. How many possible paths are there for the robot?

FOLLOW UP

Imagine certain squares are “off limits”, such that the robot can not step on them. Design an algorithm to get all possible paths for the robot.

一个NxN的矩阵，从左上角开始，每次只能向下后者向右走，如果能走到右下角则算作一个完整路径。路径上可能有地雷，有的地方不能走，在这样的限制下，输出所有可能路径。

这种有关图的题，用递归是很有用的。

递归返回条件

1.遇到了地雷，则返回
2.到达了右下角，输出路径，返回

参数设计，每一层递归的坐标向右，向下递增，将路径存储到一个公有数组变量上。

具体实现如下。


	void print_path(int m,int n,int M,int N,int len)
	{
		if(g[m][n] == 0)
			return ;
		point p ;
		p.x = m;
		p.y = n;
		vp[len++] = p;
	
		if(m == M && n == N)
		{
			for(int i = 0;i < len;i++)
				cout << "(" << vp[i].x << 	"," << vp[i].y << ")" <<  " ";
			cout << endl;	
		}
		else 
		{
			print_path(m+1,n,M,N,len);
			print_path(m,n+1,M,N,len);
		}
	}
