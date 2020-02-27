---
title: "Spark Rdd"
date: 2020-01-18T16:03:05+08:00
draft: true
tags: [Hadoop, Spark, BigData]
slug: "Spark-Rdd"
toc: false
weight: 40
summary: Spark RDD 簡單介紹
---

## pyspark shell

```bash
root@node3:/# pyspark
Python 2.7.17 (default, Nov  7 2019, 10:07:09)
[GCC 7.4.0] on linux2
Type "help", "copyright", "credits" or "license" for more information.
2020-02-26 13:55:55 WARN  NativeCodeLoader:60 - Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
Setting default log level to "WARN".
To adjust logging level use sc.setLogLevel(newLevel). For SparkR, use setLogLevel(newLevel).
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /__ / .__/\_,_/_/ /_/\_\   version 2.4.0
      /_/

Using Python version 2.7.17 (default, Nov  7 2019 10:07:09)
SparkSession available as 'spark'
```

```bash
>>> from  pyspark.sql.types import IntegerType
>>> struct1 = StructType([StructField("f1", IntegerType(), True),
...             StructField("f2", IntegerType(), True),
...             StructField("f3", IntegerType(), True),
...             StructField("f4", IntegerType(), True)])
>>> df = spark.read.csv("hdfs://172.18.1.1:9000/user/hadoop/test/",schema=struct1)
```

## Reference

- <https://codertw.com/程式語言/624829/>
