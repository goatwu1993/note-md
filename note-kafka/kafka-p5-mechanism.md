---
title: "Kafka mechanism"
slug: "kafka-p5-mechanism"
summary: "Kafka mechanism"
# basic configs
date: 2020-01-30
draft: false
tags: [hadoop, kafka, bigdata]
# other configs
diagram: true
toc: true
weight: 40
---

## Kafka Architecture

![Picture from wiki](https://upload.wikimedia.org/wikipedia/commons/thumb/6/64/Overview_of_Apache_Kafka.svg/1920px-Overview_of_Apache_Kafka.svg.png)

## Producer

### Producer 連接

### Producer 發送訊息時

- Zookeeper / bootstrap server
- Topics
- Key(可為 Null)
- Value(可為 Null)

## Broker

- Topic 被分為多個 Partition
- Partition 會有多個 Replica

- Broker controller
  - 其中一個 Broker 會被推選為 Controller
  - 負責偵測 Broker 級別的 Failure，幫忙所有受影響的 Partition 更換 Partition Leader

## Message

- Kafka 的訊息為鍵值對，使用鍵值對可以提供 Key -> Partition -> Offset 的查詢

## Topic

- Topic 為訊息的抽象分類
- Producers 發送訊息時，會指定一至多個 Topics。Consumers 訂閱一或多個 Topics
- Topics 分為 Regular Topics 及 Compacted topics
- Regular Topics 需要設定 retention time，超過則 Kafka 可刪除資料以釋出硬碟空間
- Compacted Topics 則訊息沒有有效期限，唯若 Key 重複，新訊息會覆蓋舊的訊息。Producer 可發送值為 null 的鍵值對以永久刪除該資料，稱作 tombstone message

## Partition

- 建立 Topic 時需要指定 Partitions 數目，之後只能增加不能減少
- Partition 是 Queue，訊息按 offset 嚴格排序，新訊息被 append 至尾端
- 由於是磁碟的連續區域，因此效率很高

### Partition offset

- 訊息在 partition 裡面的 index，稱作 offset，為 Long 型態的整數

## Replica

- Partition 產生 n 個副本，分散至各個 Broker 上，n 稱作 replication-factor
- 成功同步的 Replica 稱作 [ISR](#ISR)

### Partition Leader

- Broker Controller 對每個 Partition 指定一個 Leader
- Partition Leader 負責接收資料，接收並寫入後，將資料 replicate 到全部 replica/partition follower

- ### Partition Follower

  - 同一 Partition 的 non-leader replica
  - 概念上為只追隨某個 partition 的 Consumer，只 subscribe partition Leader，發現更新時 pull 到本地端
  - 當 Partition Leader 失效，Broker Controller 從 ISR 中選出新 Leader

- ### ISR

  - 當 Leader 收到訊息時，所有 Follower 都需要寫入，已經更新至和 Leader 同步的 Followers 稱為 ISRs(in-sync replica)
  - Record 只有在全部的 ISR 都同步時，才被視為成功 Commited
  - Consumer 只能從已經 Commit 成功的 Record 讀取紀錄
  - 對於一個 Topic，只要各個 Partition 皆有一個 ISR 在線，則內容保持一致且服務不中斷

## Kafka Cluster

- n 個 Broker 組成 Cluster
- 可以 zero downtime 擴展

## ZooKeeper

- 管理叢集配置
- 負責管理及協調 Broker
- 通知 Producer 及 Consumer
  - 新的 Broker 出現
  - Broker failure
- 當 Zookeeper 發出通知，Consumer 及 Producer 根據通知決定要使用哪一個 Broker
- [https://zookeeper.apache.org/](https://zookeeper.apache.org/)

## References

- <https://github.com/abhioncbr/Kafka-Message-Server/wiki/Apache-of-Kafka-Architecture-(As-per-Apache-Kafka-0.8.0-Dcoumentation)>
- <https://medium.com/@poyu677/apache-kafka-簡易入門-db58898a3fab>
- <http://cloudurable.com/blog/kafka-architecture-topics/index.html>
