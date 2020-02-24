---
title: "What is a Data Pipeline"
slug: "what-is-a-data-pipeline"
summary: "What is a Data Pipeline"
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

## 資料需要被移動

現在大家已經發現 Data 可以做許多事情了，但是通常不會在資料產生的地方去分析資料(通常有可能是服務後端)，理由如下

- 分析資料是需要效能的，在服務上面跑，有可能產生服務品質下降，或是分析速度變慢的風險。

- 初始的資料，未經過處理，通常是不太適合直接拿來做分析的，需要經過一定的轉換，而多個服務上面產生的資料，要標準化城一樣的格式，通常是比較麻煩的

- 你可能不希望服務後端的工程師可以有分析資料的權限，反之亦然

- 當你需要轉換資料格式的時候，你會希望在一個分離的系統上面來做這件事

### Data Pipelines

移動資料需要許多步驟，複製資料、搬移資料、轉換資料格式或是和其他資料合併，這些通常都是必須的，而且需要的是不同的工具。

Data Pipeline 就是這一系列工具組成的流水線，Data Pipeline 的工程師需要確保這些動作可靠地套用在全部的資料上。

市面上這麼多的 Data Pipeline 工具，代表 DP 是有可能有缺陷的，常發生的問題如下

- 當前方的服務更新時，資料格式(Scheme)也會更動，DP 有可能無法面對這種新的 schema ，或更糟：產生錯誤的資料
- 如果資料分析的結果，需要新的 Schema/欄位，DP 有可能需要更動
- 即使 Script 都正確，還是會有許多小問題，需要一個方法可以快速地找出問題，還要能夠快速的回復服務以及失去的資料。

一個好的 DP 像水管：安靜、可靠的在背景執行，但是出錯了你可能需要有人可以 On-call/On-site

## ETL Pipeline

ETL/ELT，指的是 Extract, Load, Transform，通過這三個動作將 Data 從系統/服務上面搬到 DB/DWH

## 差別在哪裡

ETL Pipeline 可以說是 Data Pipeline 的子集合，現在一般講到 ETL Pipeline，意思是資料是以批次來處理的，也就是可能每隔一段時間才會進行一次 ETL，Data Pipeline 則有可能是批次的，也有可能是 Real-Time 的(或許是通過 Streaming 的方式)

## What is Kafka used for

## How does Kafka works

## Reference

- <https://www.alooma.com/answers/what-is-the-difference-between-a-data-pipeline-and-an-etl-pipeline>

- <https://www.dremio.com/what-is-a-data-pipeline/>
