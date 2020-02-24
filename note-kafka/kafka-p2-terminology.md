---
title: "Some of Kafka terminology"
slug: "kafka-p2-terminology"
summary: "Kafka terminology"
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

---

## Producers

- 負責將訊息 push 到 Kafka cluster，任何實作 Producer API 的 Client

## Consumers

- 從 Kafka cluster pull 訊息，任何實作 Consumer API 的 Client
- **Consumer group**: 多個 Consumer 可組成 Consumer group

## Brokers

- **Broker**: Kafka 的單一節點稱作 Broker
- **Kafka Cluster**: 多個 broker 組成 Kafka Cluster
- Broker 可以說是 Apache Kafka 的 Server 端，仲介處理 Client(Consumer 以及 Producer)的訊息

## Message

- Kafka 的訊息為鍵值對，提供 Topic + Key 對 Partition 的查詢

## Topic

- Topic 為訊息的抽象分類
- Producers 發送訊息時指定 Topic
- Consumers 訂閱 Topic
- Topic 被分為多個 Partition
- Partition 會有多個 Replica

## Partition

- 建立 Topic 時需要指定 Partitions 數目，Topic 會被分為多個 Partition，Partition 數目之後只能增加不能減少

- **Partition offset**: 訊息在 partition 裡面的 index，稱作 offset，為 Long 型態的整數

## Replica

- **replication-factor**: Partition 產生 n 個副本，分散至各個 Broker 上
- **ISR**: 成功同步的 Replica 稱作 ISR
- Replica 用於保證分散式系統的高可用

---

## ZooKeeper

- Apache 的另一個分散式專案，可管理系統配置
- 負責 Kafka 的以下功能
  - 儲存 metadata
  - 選舉 controller/leader
  - Consumer group 發生變化時，進行 rebalance
  - 當 Producer 指定 ZK(而非 bootstrap server)，ZK 負責返回 broker list
- Kafka Improvement Proposals 已經通過，將 Zookeeper 從 Kafka 移除，使用 bootstrap server/broker controller/共識來維護 Kafka ，<https://cwiki.apache.org/confluence/display/KAFKA/KIP-500%3A+Replace+ZooKeeper+with+a+Self-Managed+Metadata+Quorum>

## References

- <https://github.com/abhioncbr/Kafka-Message-Server/wiki/Apache-of-Kafka-Architecture-(As-per-Apache-Kafka-0.8.0-Dcoumentation)>
- <https://medium.com/@poyu677/apache-kafka-簡易入門-db58898a3fab>
- <http://cloudurable.com/blog/kafka-architecture-topics/index.html>
- <https://gitbook.cn/books/5ae1e77197c22f130e67ec4e/index.html>
