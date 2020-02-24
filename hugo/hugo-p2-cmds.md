---
title: "Hugo commands"
date: 2019-12-27T21:32:52+08:00
draft: false
tags: [hugo, commands]
slug: hugo-commands
summary: hugo basic commands
---

## Hugo 使用

### 安裝

```bash
brew install hugo
```

### 第一次使用

```bash
hugo new site quickstart
```

### 測試

```bash
#!/bin/bash
cd quickstart
hugo
hugo server
```

### 部署

注意 content 寫完輸入 hugo 並不會自動刪除目標資料夾，手動刪除再跑一次 hugo 。

```bash
rm -rf ./docs
hugo
```

### 新增文章

```bash
hugo new posts/my-first-post.md
```

### References

- [Hugo 官網](https://gohugo.io/getting-started/quick-start/)
