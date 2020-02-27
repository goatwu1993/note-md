---
title: "What is hive"
slug: "what-is-hive"
summary: "Hive brief introduction"
# basic configs
date: 2020-02-27
draft: false
tags: [hive, bigdata]
# other configs
diagram: true
toc: true
weight: 40
---

## What is HiveQL

```bash
hive>create schema if not exists test;

hive>create external table if not exists test.test_data (row1 int, row2 int, row3 decimal(10,3), row4 int) row format delimited fields terminated by ',' stored as textfile location 'hdfs://172.18.1.1:9000/user/hadoop/test/';

hive>select * from test.test_data where row3 > 2.499;
SELECT * FROM test.test_data WHERE row3 > 2.499;
```

## References

- <https://github.com/sciencepal/dockers/tree/master/hadoop_hive_spark_docker>
- <http://tw.gitbook.net/hive/hiveql_select_where.html>
