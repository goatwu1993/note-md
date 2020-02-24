---
title: "Hugo themes"
date: 2019-12-27T21:32:52+08:00
draft: false
tags: [hugo, git]
slug: hugo-themes
summary: " "
---

本篇記錄如何使用 hugo 線上的 themes

## 更正

如果需要覆蓋 layouts 的話可以直接在根目錄下面建立一個 layouts 資料夾，裡面的內容會 override themes/name/layouts 底下的。

## Hugo themes

[Hugo 官方線上 themes](https://themes.gohugo.io/)

### a. 直接 submodule

~~不考慮更改 themes 的 partial/layout/css 的話，直接照抄就好~~
如果不太更動 theme 或是內容比較一般性的話，可以直接 clone。

```bash
# submodule
cd ./themes
git submodule add https://github.com/avianto/hugo-kiera.git kiera
```

### b. fork 再 submodule

如果需要更改一些比較客製化的版本的話請選擇 fork。

```bash
# fork
cd ./themes
git clone https://github.com/$你的Id/hugo-kiera.git kiera
```

## 修改 config.toml

```bash
theme = "kiera"
```
