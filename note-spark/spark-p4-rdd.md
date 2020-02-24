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

## What is RDD

RDD(Resilient Distributed Datasets)
RDD 就是我們常見的集合概念，比較特別的是實際資料集可以為橫跨數個結點所組成。

### RDD 是什麼

- RDD 是 Spark 的抽象 Dataset
- RDD 上面可以進行兩種操作：Transfromation & Action
- RDD 會記錄本身是如何從原始資料得出的，稱為 Lineage
- 支援 Scala, Java 和 Python API ，方法類似操縱本地端的資料庫。
- 支援 long, int 及 String 形態
- RDD 運算分為 Transform 及 Action

```mermaid
Core --> RDD(RDD)
Core --> DataFrame(DataFrame)
Core --> Dataset(Dataset)
RDD --> RDD1(Transformation)
RDD --> RDD2(Action)
```

## RDD 特性

1. 不可更動(Immutable)  
   要讓資料容易用於分散式系統，Immutable 是關鍵的一環。
2. 彈性(Resilient)  
   分散式環境中忽然有節點失效是正常的，配合 RDD lineage 可以做各種推算。

## RDD Lineage

要紀錄了操作與建立行為(有點類似 DB 的 commit log)，child RDD 就可以從 parent RDD 取得，因此可以串出 RDD 間的關係，例如： line -> badLines -> OtherRDD1 -> OtherRDD2 -> ...。

我們將其稱為 RDD lineage(族譜)。所以假設存放 badLines RDD 的節點損毀了(一或多台)，但只要儲存 line RDD 的節點還在的話，是不是就能還原 badLines 了呢！當然底層通常會搭配一個分散式並且有副本(replication)特性的儲存系統，例如常見的 Hadoop HDFS 或 S3 等。

## RDD 運算

## Referencce

- <https://ithelp.ithome.com.tw/articles/10186282>
