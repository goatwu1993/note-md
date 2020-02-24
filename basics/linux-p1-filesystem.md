---
title: "Linux filesystem"
date: 2019-12-28T19:17:18+08:00
draft: false
diagram: false
tags: [linux]
slug: linux-p1-filesystem
toc: true
weight: 40
summary: Linux File system
---

## /bin

- 系統基礎的 Binary 檔案，如: ls, mv, rm, mkdir, rmdir 常用的執行檔
- 內容和/usr/bin 基本相同，有時候會使用連結檔

## /home

- Contains user's home directory

## /dev

- Devices，裝置相關的檔案或特殊的檔案
- Unix 或 Linux 系統均把裝置當成是一個檔案來看待

## /etc

- 存放 Host 以及系統的設定檔，通常
  是靜態的檔案，並且不會放 binary 或可執行檔

### /etc/init.d

- 啟動腳本以及服務腳本

### /etc/rc.d

- 記錄一些開關機過程中的 scripts 檔案， scripts 有點像是 DOS 下的批次檔

### /etc/opt

## /lib

- Shared Library and kernal modules

## /lib64

- Shared Library and kernal modules(x64)

## /mnt

- Mounting point of a filesystem.

## /proc

- Kernal data structure mounted as a filesystem. Only applicable to Linux based OS

## /root

系統管理員的目錄

## /sbin

- System Binaries 及執行檔
- /sbin/shutdow，關機指令
- /sbin/fastboot
- /sbin/reboot

## /tmp

- Used for storing temporary data and files

## /var

- 時常會更動的檔案

## /usr

### /usr/bin

### /usr/local

### /usr/local/bin

## References

- <https://linux.vbird.org/linux_basic/redhat6.1/linux_05file.php>
- <https://unix.stackexchange.com/questions/4186/what-is-usr-local-bin>
- <http://www.pathname.com/fhs/>
