---
title: "Data pipeline Basics"
slug: "p2-data-pipeline-basics"
summary: "Data pipeline basics"
# basic configs
date: 2020-02-12
Lastmod: 2020-02-12
draft: true
tags: [data]
# other configs
diagram: true
toc: true
weight: 40
---

## What is Data Pipeline

Data Pipeline 是一個比較通俗的說法，任何工具只要能夠搬運 Data 的，都可以叫做 Data Pipeline

## ETL Pipeline

ETL/ELT，指的是 Extract, Load, Transform，通過這三個動作將 Data 從系統/服務上面搬到 DB/DWH

## 差別在哪裡

ETL Pipeline 可以說是 Data Pipeline 的子集合，現在一般講到 ETL Pipeline，意思是資料是以批次來處理的，也就是可能每隔一段時間才會進行一次 ETL，Data Pipeline 則有可能是批次的，也有可能是 Real-Time 的(或許是通過 Streaming 的方式)

## What is Kafka used for

## How does Kafka works

## Reference

- <https://www.alooma.com/answers/what-is-the-difference-between-a-data-pipeline-and-an-etl-pipeline>

- <https://www.dremio.com/what-is-a-data-pipeline/>
