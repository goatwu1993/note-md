---
title: "Kafka + ELK"
slug: "kafka-elk"
summary: "Kafka+ELK"
# basic configs
date: 2020-01-30
Lastmod: 2020-02-12
draft: false
tags: [hadoop, kafka, bigdata]
# other configs
diagram: false
toc: true
weight: 120212
---

## Repos

<https://github.com/wurstmeister/kafka-dockers>

## 環境

- macOS Catalina 10.15.3
- kafka 2.4.0 (installed by Homebrew)
- Docker Desktop 2.2.0.0

## 準備 Image

- wurstmeister/zookeeper
- wurstmeister/kafka
- sebp/elk

```bash
docker pull wurstmeister/zookeeper
docker pull wurstmeister/kafka
docker pull sebp/elk
```

## Zookeeper

```bash
docker run --name zk -p 2181:2181 -p 2888:2888 -p 3888:3888 --restart always -d zookeeper
```

## Kafka

```bash

docker run -d --name kafka -p 9092:9092 --link zk --env KAFKA_ZOOKEEPER_CONNECT=zk:2181 --env KAFKA_ADVERTISED_HOST_NAME=${host_ip} --env KAFKA_ADVERTISED_PORT=9092 wurstmeister/kafka
```

開個 Topics 測試一下

```bash
host_ip="HOST_IP"

kafka-topics --create --zookeeper ${host_ip}:2181 --replication-factor 1 --partitions 1 --topic elk_test

kafka-topics --describe --zookeeper ${host_ip}:2181
```

不放心的話再寫個訊息

```bash
kafka-topics --create --zookeeper ${host_ip}:2181 --replication-factor 1 --partitions 1 --topic kfk_test

kafka-console-producer --broker-list ${host_ip}:9092 --topic kfk_test
>
# 輸入
# Control+C 關掉

kafka-console-consumer --topic=kfk_test --bootstrap-server=${host_ip}:9092 --from-beginning
```

## ELK

Elasticsearch 好像很吃 Memory

```bash
screen /Users/peteeelol/Library/Containers/com.docker.docker/Data//vms/0/tty

sysctl -w vm.max_map_count=262144
```

```bash
docker run -d -p 5601:5601 -p 9200:9200 -p 9300:9300 -p 5044:5044 -e ES_MIN_MEM=128m -e ES_MAX_MEM=2048m -it --name elk sebp/elk
```

檢查

```bash
# Kibana
open http://"${host_ip}":5601

# docker
$ docker exec elk jps
105 Elasticsearch
313 Logstash
415 Jps
```

## 設定 Logstash

### 簡單測試

```bash
$ docker exec -it elk /bin/bash

service --status-all

service logstash stop

/opt/logstash/bin/logstash -e 'input { stdin { } } output { elasticsearch { hosts => ["localhost"] } }'
...
...
...
Hello
# Control + C 離開stdin
```

最後一個指令需要跑一下，接著輸入一些訊息

離開 Docker 用 Host(Mac) 打開瀏覽器

```bash
open http://localhost:9200/_search?pretty
```

應該要能看到剛剛 stdin 輸入的訊息

### 設定檔

回到 Container elk

```bash
vim /etc/logstash/conf.d/kafka.conf
```

```bash
input {
    kafka {
        bootstrap_servers => ["HOST_IP:9092"]
        group_id => "test-consumer-group"
        auto_offset_reset => "latest"
        consumer_threads => 5
        decorate_events => true
        topics => ["elk_topics"]
        type => "bhy"
    }
}

output {
    elasticsearch {
        hosts => ["http://localhost:9200"]
        index => "myservice-%{+YYYY.MM.dd}"
        #user => "elastic"
        #password => "changeme"
    }
}
```

### 更改 Logstash 權限

```bash
vim /etc/init.d/logstash
```

將 LS_USER, LS_GROUP 更改為 root

```vim
LS_USER=root
LS_GROUP=root
```

再把 Logstash 重跑

```bash
service logstash restart
```

這時候 Logstash 應該就有在接收 Kafka 的 elk_topics 這個 Topic 了，可以用 Host 發送訊息測試看看

```bash
kafka-console-producer --broker-list ${host_ip}:9092 --topic elk_topics
```

在 Kibana 應該要看到 index 為 my-service 開頭的訊息，代表訊息透過 Kafka-> Logstash -> Elastic Search

## References

- <https://medium.com/@poyu677/apache-kafka-%E7%B0%A1%E6%98%93%E5%85%A5%E9%96%80-db58898a3fab>

- <https://github.com/wurstmeister/kafka-docker/wiki/Connectivity>

- <https://github.com/sermilrod/kafka-elk-docker-compose>
