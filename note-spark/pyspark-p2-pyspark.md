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
root@node2:/# pyspark --version
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /___/ .__/\_,_/_/ /_/\_\   version 2.4.0
      /_/

Using Scala version 2.11.12, OpenJDK 64-Bit Server VM, 1.8.0_242
Branch
Compiled by user  on 2018-10-29T06:48:44Z
Revision
Url
Type --help for more information.

```

2.0.0 以後 Spark 建議大家使用 SparkSession(pyspark.sql.session.SparkSession) 來編寫程式，取代
SparkContext

```bash
root@node2:/# pyspark
```

## Create SparkContext

```python
from pyspark import SparkContext, SparkConf

conf = SparkConf().setAppName("myFirstApp").setMaster("local")
sc = SparkContext(conf=conf)
```

## Create RDD

### Assign from array

```python
## Array
data = [1, 2, 3, 4, 5]
distData = sc.parallelize(data)
```

### External Datasets (HDFS)

```python
## HDFS
textFile = sc.textFile("hdfs://172.18.1.1:9000/user/hadoop/test/")
```

### External Datasets (file)

```python
distFile = sc.textFile("data.txt")
```

## Check

```python
textFile.first()
textFile.take(5)
```

## Reference

- <https://spark.apache.org/docs/latest/rdd-programming-guide.html>
