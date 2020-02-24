---
title: "Kafka with multi brokers"
slug: "kafka-p4-multibrokers"
summary: "Kafka macOS hands-on, multi brokers"
# basic settings
draft: false
tags: [hadoop, kafka, bigdata]
date: 2020-01-30
Lastmod: 2020-02-10
# other configs
diagram: true
toc: true
weight: 40
---

## Prerequisite

```bash
# this will install java 1.8, zookeeper, and kafka
brew install kafka
```

## 啟動 zookeeper

```bash
brew services start zookeeper
```

## 開啟三個 Brokers

分别修改 server1.properties, server2.properties

| 修改位置  | server.properties                       | server1.properties                      | server2.properties                      |
| :-------: | --------------------------------------- | --------------------------------------- | --------------------------------------- |
| broker.id | broker.id=0                             | broker.id=1                             | broker.id=2                             |
| listeners | listeners=PLAINTEXT://:9092             | listeners=PLAINTEXT://:9093             | listeners=PLAINTEXT://:9094             |
|  log.dir  | log.dir=/usr/local/var/lib/kafka-logs-0 | log.dir=/usr/local/var/lib/kafka-logs-1 | log.dir=/usr/local/var/lib/kafka-logs-2 |

```bash
kafka-server-start /usr/local/etc/kafka/server.properties &
kafka-server-start /usr/local/etc/kafka/server1.properties &
kafka-server-start /usr/local/etc/kafka/server2.properties &
```

## 開啟一個兩個副本的 Topic

```bash
kafka-topics –create –zookeeper localhost:2181 –replication-factor 3 –partitions 1 –topic mytopic
```

## Consumer & Producer API

- Shell script  
  使用 brew kafka 提供的 shell script
- Python
  - pykafka
  - kafka-python
- Scala
  - Scala-Shell
  - Native-App

## Shell Script

開啟兩個命令列

```bash
./bin/kafka-console-producer --broker-list localhost:9092 --topic test-kafka
```

```bash
./bin/kafka-console-consumer --bootstrap-server localhost:9092 --topic test-kafka --from-beginning
```

應該要能看到訊息傳送過去

## References

- <https://oumuv.github.io/2018/12/06/kafka-2/>
- <https://blog.v123582.tw/2019/03/27/在-mac-上建立-Python-的-Kafka-與-Spark-環境/>
