---
title: "Kafka with single broker"
slug: "kafka-p3-singlebroker"
summary: "Kafka macOS hands-on"
# basic configs
date: 2020-01-30
draft: false
tags: [hadoop, kafka, bigdata]
# other configs
diagram: true
toc: true
weight: 40
---

## Install Kafka

```bash
# this will install java 1.8, zookeeper, and kafka
brew install kafka
```

檔案位置

- /usr/local/etc/kafka
- /usr/local/Cellar/kafka/\$版號

```bash
cd /usr/local/Cellar/kafka/*
# 啟動zookeeper
./bin/zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties
# 啟動kafka
./bin/kafka-server-start /usr/local/etc/kafka/server.properties
# 建一個名為 test-kafka 的 Topic
./bin/kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test-kafka

# 查看目前已經建立過的 Topic
./bin/kafka-topics --list --zookeeper localhost:2181\n\n
```

## 啟動 zookeeper & kafka

```bash
brew services start zookeeper
brew services start kafka
```

## Consumer & Producer API 選擇

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

console1

```bash
kafka-console-producer --broker-list localhost:9092 --topic test-kafka
```

console2

```bash
kafka-console-consumer --bootstrap-server localhost:9092 --topic test-kafka --from-beginning
```

應該要能看到 console1 的輸入

## References

- <https://oumuv.github.io/2018/12/06/kafka-2/>
- <https://blog.v123582.tw/2019/03/27/在-mac-上建立-Python-的-Kafka-與-Spark-環境/>
