---
title: "Bash - source & export"
date: 2020-01-20T19:09:20+08:00
draft: false
diagram: true
tags: [shell, bash]
slug: "bash-p5-source-export"
toc: true
weight: 40
summary: bash source, execute and export life cycle.
---

## source

使用 source 執行 shell script 會直接沿用目前的進程。

```bash
source hello-world.sh
```

## excute

直接執行 shell script 會開啟一個子進程

```bash
./hello-world.sh
```

## export

將某個變數變成環境變數，Life cycle 為這個進程結束為止

## diagram

```mermaid
graph TD
    subgraph Export Life cycle
        C1(parent process) -.-> |sleep| C2(parent process)
        C1 --> C3(export foo=FOO)
        C3 --> C4(echo $foo <br> FOO)
        C4 --> |export expire|C2
    end
    subgraph Execute
        A1(parent process) -.-> |sleep| A2(parent process)
        A1 --> |fork| A3(test1.sh)
        A3 --> A2
    end
    subgraph Source
        B1(parent process) -.-> B2(test1.sh)
        B2 -.-> B3(child process)
    end
```

## References

- <https://superuser.com/questions/176783/what-is-the-difference-between-executing-a-bash-script-vs-sourcing-it>
