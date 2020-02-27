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

## Create SparkSession

```python
import findspark
findspark.init()

from pyspark.conf import SparkConf
from pyspark.sql import SparkSession
from pyspark.sql import SQLContext

conf = SparkConf().setAppName("PySpark App").setMaster("spark://master:7077")

spark = spark = SparkSession.builder.config(conf=conf).getOrCreate()
```
