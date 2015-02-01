---
author: bydiao
comments: true
date: 2013-11-25 09:59:44+00:00
layout: post
slug: crack-the-coding-interview8-3
title: Crack the coding interview:8-3 8-4
wordpress_id: 555
categories:
- 面试题
tags: [面试题]
---

Write a method that returns all subsets of a set.

得到一个数组的所有子集合，及一个幂集。

这个方法之前提到过，有一个生成组合数的算法，可以得到幂集，同样也可以用一个数递增，然后用位运算得到组合数。二者思路一样，实现不同而已。

另一个想法是用递归实现，从集合中依次去掉一个元素求幂集，递归的边界返回条件是去掉了所有元素，返回一个空集。
递归返回后，依次将上一层得到的所有集合与当前去掉的元素求并，得到新的集合与上一层返回的集合合并，返回给上一层。
这样就得到了最终的幂集，函数实现代码如下：


	vvi get_subsets1(int a[], int idx, int n){
    vvi subsets;
    if(idx == n){
        vi subset;
        subsets.push_back(subset); //empty set
    }
    else{
        vvi rsubsets = get_subsets1(a, idx+1, n);
        int v = a[idx];
        for(int i=0; i<rsubsets.size(); ++i){
            vi subset = rsubsets[i];
            subsets.push_back(subset);
            subset.push_back(v);
            subsets.push_back(subset);
        }
    }
    return subsets;
}


递归的参数的设计和边界条件的讨论是核心

8-4则是返回一个字符串的所有排列数，思路同上，但细节上有所不同

abcd为例，递归返回条件相同
返回后的操作，是将当前下标的字符，插入到返回的数组中

例如最后一层返回d，则有cd和dc，返回到上一层则有bcd，cbd，cdb和bdc，dbc，dcb，再到上一层，一共24个排列字符串。
