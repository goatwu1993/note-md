---
title: "Bash - ownership"
date: 2020-01-19T22:11:15+08:00
draft: true
diagram: false
tags: [shell, bash]
slug: "bash-p2-ownership"
toc: true
weight: 40
---

## Linux is a Multiuser, Multitasking Operating System

**Multiuser**: 多個使用者可以同時取用系統的資源(算力/磁碟空間)，並且不應該互相影響。

**Multitasking**: 處理器可以同時處理多個 Task，實際上勢將處理器的時間切分，執行一小段時間的 Task 就跳到下一個。

## UID/GID

為了達成 Multiuser 的目標，Linux 將每個使用者給予兩個標籤

- User ID (UID): 特殊且唯一
- Group ID (GID): 一個使用者可會有唯一的 Primary Group，GID 即是 Primary Group 的 ID
- Groups: 一個使用者可以屬於多個 Group

針對每個 GID+UID，會產生 3 種不同的使用者

- UID 相同: 本人
- UID 不同，GID 相同: 同個群組的人
- UID 和 GID 皆不同: 任何人

### 顯示 GID/UID

```bash
# Get user/group information
id
# Get UID
id -u
# Get user name
id -un
# Get Primary Group
id -g
# Get Primary Group
id -gn
# Get all groups you belong
groups
```

### 創建檔案時會自動套用 GID/Primary Group

```bash
bash-3.2$ touch file1
bash-3.2$ dir1
bash-3.2$ ls -la
total 0
drwxr-xr-x   4 peteeelol  staff   128 Feb 17 21:24 .
drwxr-xr-x@ 37 peteeelol  staff  1184 Feb 14 18:42 ..
drwxr-xr-x   2 peteeelol  staff    64 Feb 17 21:24 dir1
-rw-r--r--   1 peteeelol  staff     0 Feb 17 21:23 file1

```

### 更改檔案的 GID/UID

```bash
# Change ownership of a file.
chown
# Change an ownership of a file.
chown nobody.nogroup your_file_name
# Recursively change all file under this directory.
chown -R nobody.nogroup .
```

## 權限管理

## 檔案的權限

一個檔案會儲存

- GID
- UID

並根據 GID/UID 分類成的 3 種使用者，做以下三個動作的權限管理

- 讀取(Read)
- 寫入(Write)
- 執行(Execute)

### 顯示檔案權限

```bash
$ ls -la ~/.zshrc
lrwxr-xr-x    1 peteeelol  staff    22B Jan  6 16:41 .zshrc -> my-dotfiles/zsh/.zshrc
```

- **l**: 檔案種類，l 代表這是連結檔
- **rwx**: UID 相同的人可以讀+寫+執行
- **r-x**: GID 相同的人可以讀+執行
- **r-x**: 任何人可以讀+執行

### 預設權限 Umask

當檔案被創建，檔案會給予 Default 的權限，如果為資料夾，則權限為 755-umask，檔案則為 644-umask

```bash
umask
022
```

則創建資料夾會給予 733 的權限，創建檔案則會給予 622 的權限

### 更改檔案權限

```bash

# Change the read/write permission of a file
chmod
# Make file r/w/e able for all user & group.
chmod 777 file1
```

## Referencce

- <http://linux.vbird.org/linux_basic/0410accountmanager.php>
