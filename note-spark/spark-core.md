---
title: "Spark Core"
date: 2020-01-18T15:50:14+08:00
draft: true
tags: []
slug: "Spark-Core"
toc: false
weight: 40
---

## Core API

## 匿名函式

```bash
scala> val lines = sc.textFile("./content/posts/hadoop/kafka-p1.md")
lines: org.apache.spark.rdd.RDD[String] = ./content/posts/hadoop/kafka-p1.md MapPartitionsRDD[1] at textFile at <console>:24

scala> def isKFK(line:String) = { line.contains("kafka")}
isKFK: (line: String)Boolean

scala> val kfkLines = lines.filter(isKFK)
kfkLines: org.apache.spark.rdd.RDD[String] = MapPartitionsRDD[3] at filter at <console>:27

scala> kfkLines.count
res0: Long = 1
```

可以將 isKFK 的宣告省略，直接傳遞匿名函數給 lines.filter

```bash
scala> val lines = sc.textFile("./content/posts/hadoop/kafka-p1.md")
lines: org.apache.spark.rdd.RDD[String] = ./content/posts/hadoop/kafka-p1.md MapPartitionsRDD[1] at textFile at <console>:24

scala> val kfkLines = lines.filter(line=>line.contains("kafka"))
kfkLines: org.apache.spark.rdd.RDD[String] = MapPartitionsRDD[2] at filter at <console>:25

scala> kfkLines.count
res0: Long = 1
```

## filter

```bash
scala> val lines = sc.textFile("./content/posts/hadoop/kafka-p1.md")
lines: org.apache.spark.rdd.RDD[String] = ./content/posts/hadoop/kafka-p1.md MapPartitionsRDD[1] at textFile at <console>:24

scala> val kfkLines = lines.filter(line=>line.contains("kafka"))
kfkLines: org.apache.spark.rdd.RDD[String] = MapPartitionsRDD[2] at filter at <console>:25

scala> kfkLines.count
res0: Long = 1
```

## foreach

```bash
scala> kfkLines.foreach(kline=>println(kline))
slug : "kafka-p1"

scala> kfkLines.foreach(println)
slug : "kafka-p1"
```

(line=>line.contains("kafka"))代表導入一個 Scala 匿名函式，其輸入為 line 字串，
輸出為 line.contains("kafka")的布林值。若為真則被濾出。結果會寫入另外一個 immutable 的變數 kfkLines 中(Scala 中 val 為 immutable;var 為 mutable)。

## Referencce

- <https://ithelp.ithome.com.tw/articles/10186152>
