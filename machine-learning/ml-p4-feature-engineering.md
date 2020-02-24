---
title: "ML-Feature-Engineering"
date: 2020-01-16T20:24:05+08:00
draft: false
---

## PCA

- Primary Componenet Analysis
- 無監督學習
- 根據原始特徵數目 n，可以產生最多 n 個維度

## LDA

- Linear Discriminant analysis
- 監督式學習
- 根據原始分類數目 C，可以產生最多 C-1 個維度

## Comparision

|    Method    | supervised / unsupervised | linear / non-linear | Disk 2 | Disk 3  |
| :----------: | :-----------------------: | :-----------------: | :----: | ------- |
|     PCA      |       unsupervised        |       linear        |   A3   | Ap(1-3) |
|     LDA      |        supervised         |                     |        |         |
| Auto-Encoder |                           |     non-linear      |   A6   | Ap(4-6) |
|      B1      |                           |         B2          |   B3   | Bp(1-3) |
|      B4      |                           |         B5          |   B6   | Bp(4-6) |
