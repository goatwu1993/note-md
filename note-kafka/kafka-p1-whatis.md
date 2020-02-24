---
title: "What is Kafka"
slug: "kafka-p1"
summary: What is Apache Kafka
# basic configs
date: 2020-01-30
draft: false
tags: [hadoop, kafka, bigdata]
# other configs
diagram: true
toc: true
weight: 40
---

Kafka 是一個分散式的訊息處理平台(message processing platform)，仲介處理端到端的實時訊息傳輸。

## Kafka 特點

- **分散式**
- 可以自由調整 C/A/P
- **減少網路封包的 Overhead**: 使用優化過的 binary TCP-based protocol，多條訊息會先寫入記憶體緩衝中存成 Batch 一同傳輸，
- **輕量級可壓縮**: 避免對訊息的物件包覆，以**檔案**的型式來處理資料
- 使用 OS 的 page cache，不需要額外 Applicaion Cache ，爭取珍貴的記憶體空間

## Kafka 優點

- Reliability
- Scalability
- Durability
- Performance
- Fault Tolerance
- Zero downtime
