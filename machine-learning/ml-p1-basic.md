---
title: "Ml P1"
date: 2020-01-16T20:20:15+08:00
draft: false
diagram: true
---

## Machine Learning Categories

## Gathering Data

## Data preparation

### Data Preprocessing 資料預處理

- Handling Missing Values
- Outlier
- Feature Engineering

## Model & HyperParameter 模型及超參數

## Loss Function 損失函數

## Activation Function 激活函數

```mermaid
graph TD
A[Gathering Data] -->B[Data preparation]
B --> C[Handling Missing Values]
B --> D[Handling Outlier]
C --> E[Feature Engineering]
D --> E
E --> F[Scaling]
E --> G[One-Hot Encodi  ng]
E --> H[box-cox]
E --> I[New Feature]
F --> J[Model]
G --> J
H --> J
I --> J
```
