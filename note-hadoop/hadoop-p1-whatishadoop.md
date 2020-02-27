---
title: "What is Hadoop"
slug: "hadoop-p1-whatishadoop"
summary: "Hadoop brief introduction"
# basic configs
date: 2020-01-30
draft: false
tags: [hadoop, bigdata]
# other configs
diagram: true
toc: true
weight: 40
---

## What is Hadoop

Apache Hadoop 是一款支援資料密集型分布式應用程式並以 Apache 2.0 許可協定發布的開源軟體框架。它支援在商品硬體構建的大型叢集上運行的應用程式。Hadoop 是根據 Google 公司發表的 MapReduce 和 Google 檔案系統的論文自行實作而成。所有的 Hadoop 模組都有一個基本假設，即硬體故障是常見情況，應該由框架自動處理。

Hadoop 框架透明地為應用提供可靠性和資料移動。它實現了名為 MapReduce 的編程範式：應用程式被分割成許多小部分，而每個部分都能在叢集中的任意節點上執行或重新執行。此外，Hadoop 還提供了分布式檔案系統，用以儲存所有計算節點的資料，這為整個叢集帶來了非常高的帶寬。MapReduce 和分布式檔案系統的設計，使得整個框架能夠自動處理節點故障。它使應用程式與成千上萬的獨立計算的電腦和 PB 級的資料連接起來。

## How Hadoop work

Hadoop 由四個組件組成

**Hadoop Distributed File System (HDFS)**
**MapReduce**: 平行計算框架
**YARN**: Yet Another Resource Negotiator.
**Hadoop Common**: 基本的工具(Java)，讓使用者或 OS 可以和 HDFS 互動

### Hadoop eco-system

Spark, HBAse, Hive, Kafka, HDFS, etc

## Referencce

- <https://zh.wikipedia.org/wiki/Apache_Hadoop>
- <https://kknews.cc/zh-tw/code/rlyqae4.html>
