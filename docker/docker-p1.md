---
title: "Docker P1"
date: 2020-02-09
draft: true
tags: [Docker]
slug: "docker-p1"
weight: 30
summary: Basic docker concept
---

## A dockerfile example

[Centos Docker](https://hub.docker.com/_/centos)

```dockerfile
FROM centos:7
ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]
```

```bash
$ docker build --rm -t local/c7-systemd .
```

## Key words

**FROM**: 指定 base image

**指定 docker 執行起來時候的預設目錄位置**: 指定 docker 執行起來時候的預設目錄位置

**CMD**: 指定 Instance 啟動後所要執行的指令

**ENTRYPOINT** : 指令 Instance 啟動後，程式的進入點

**ENV** : 指令啟動後的環境變數

### VOLUME

### CMD

## References

- <https://hub.docker.com/_/centos>
