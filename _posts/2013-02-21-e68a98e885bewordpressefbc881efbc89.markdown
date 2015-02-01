---
author: bydiao
comments: true
date: 2013-02-21 13:03:18+00:00
layout: post
slug: '%e6%8a%98%e8%85%bewordpress%ef%bc%881%ef%bc%89'
title: 折腾Wordpress 一
wordpress_id: 88
categories: [技术杂汇]
tages: [技术杂汇]
---

Wordpress作为一个通用博客平台还真是强大，简单易用，扩展丰富。用了也有一段时间，现将一些应用心得总结如下。

1.Wordpress的安装

安装非常简单，下载最新的Wrodpress，FTP上传，解压。然后访问 xxx.cn/wp-admin即可进入安装向导，根据提示一步一步安装即可。

2.选择一款主题

Wordpress提供了丰富的主题，可以根据自己的喜好选择。看过一些大牛的博客，多用NeoEase的一款主题，自己也很喜欢，遂用之。

可以再Wordpress后台直接搜索安装主题，也可以在网上找到主题压缩包，FTP上传到wp-content/themes文件夹下，解压即可在Wp后台看到主题，选择启用即可。

3.安装插件

Wp鼓励开发人员为Wp开发各种各样的插件，这也是Wp吸引人的地方之一，海量的插件增加了Wp的可用性，给Wp注入了无限的活力。

现用的主要有:

Baidu Tongji 统计小站访问量

Syntax Highlighter Evolved 语法高亮显示文章中的代码

新浪微博插件

插件也可以通过Wp后台搜索下载安装，也可以在网上找到压缩包，然后通过Wp向导安装。

4.段首缩进

由于Wp是国外开发的，所以没考虑汉语输入段首缩进的问题，中国人可以DIY一下。修改主题文件中的style.css

在#content部分加入以下代码即可：

<code>
	#content .post p {text-indent:2em;}
</code>

5.分类，归档的数量统计。

分类，归档两个小栏目也是Wp的插件，默认没有统计文章的数量，可以DIY一下

在主题目录下找到sidebar.php文件，iNove主题默认分为northsidebar，southsidebar和centersidebar，centersidebar又分成westsidebar和eastsidebar。我删掉了westbar。
默认归档是在southbar中，在wp_get_archives参数中添加show_post_count=true即可。

<code>
	<?php wp_get_archives('type=monthly&show_post_count=true'); ?>
</code>

默认分类是在eastsidebar中，在wp_list_categories中修改参数如下即可。

<code>
	<?php wp_list_categories('&title_li=&show_count=1'); ?>
</code>

6.默认字体修改

Wp默认的文章字体是12px，有点小，可以在body中修改为14px

<code>
	body {
	background:#BEC3C6 url(img/bg.jpg) repeat-x;
	color:#555;
	font-family:Verdana,"BitStream vera Sans",Tahoma,Helvetica,Sans-serif;
	font-size:14px;
	}
</code>

以上是对Wp的一些DIY，现在的页面看上去还算顺眼。主要修改的是主题目录下的style.css和sidebar.php。
Wordpress博大精深，日后如有新发现，再作总结。
