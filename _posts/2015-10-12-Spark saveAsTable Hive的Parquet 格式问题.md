---
author: bydiao
comments: true
date: 2015-10-12 
layout: post
title: Spark saveAsTable Hive的Paquet格式问题
mathjax: true
categories: [Big Data]
tags: [Spark]
---

# Spark saveAsTable Hive的Parquet 格式问题

@(Spark)

1. Serde
	Serde is short for Serializer/Deserializer. Serde 允许Hive读取和写入任意用户自定义的表格格式。
2.  Hive parquet表格和Spark saveAsTable表格的对比

	|Item|Hive|Spark|
	|---|---|---|---|
	|Prefix|org.apache.hadoop.hive.ql.io.parquet|org.apache.hadoop|
	|SerDe Library|serde.parquetHiveSerDe|hive.serde2.MetadataTypedColumnsetSerDe|
	|InputFormat|MapredParquetInputFormat|mapred.SequenceFileInputFormat|
	|OutputFormat|MapredParquetOutputFormat|hive.ql.HiveSequenceFileOutputFormat|
	
3. 显然二者是不同的，现象就是saveAsTable存的表，hive读出来全部是null。

4. spark邮件列表中，有人提到了这个问题。官方的回答是，spark的saveAsTable存成的表，就是不能通过hive访问的。如果想通过hive访问，在spark中，就需要通过sql执行。

{% highlight Scala%}
val hc = new org.apache.spark.sql.hive.HiveContext(sc)
hc.sql("create table abc as select * from xxx")
{% endhighlight %}

 因此，之前通过saveAsTable存表的思路就要改了

要通过sql来存，其他的应该后没有变化。

具体思路就是 rdd=>dataframe=>tmptable>sql create

测试可行。 