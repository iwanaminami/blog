---
layout: post
title: BrdUラベリングの時系列データからパラメータ推定
date: 2019-11-11 10:00:00 +0900
image: '/img/covers/brduestimation.png'
tags:
- research
- R
- parameter estimation
- BrdU
description: ウイルス感染と常微分方程式 (シリーズ・現象を解明する数学)の中で紹介されている、BrdUラベリングデータから常微分方程式で記述された数理モデルのパラメータを推定する方法
categories: research
---

---


## Introduction

岩見真吾他（箸）のウイルス感染と常微分方程式 (シリーズ・現象を解明する数学)を元に時系列データから数理モデルのパラメータを推定する方法を解説する。

ウイルス感染と常微分方程式 (シリーズ・現象を解明する数学)  
[https://amzn.to/2JOWl5P](https://amzn.to/2JOWl5P)

Rを使った最小二乗法によるデータフィッティングの方法に重点を置き、数理モデルの説明は最小限にする。

使用するデータは、岩見真吾, 佐藤佳, 竹内康博 (2017). 「ウイルス感染と常微分方程式」. 共立出版

---

## Materials and Methods

### Model

詳細な導出は省きますが、BrdU投与中、BrdU投与後の活性化T細胞BrdU陽性率は以下の式で表される。

$$
\begin{align*}
f_{L}\left(t\right) = 100 \alpha \left\{1-\mathrm{e}^{-\left(d-p\right)}\right\} \\
\left[ K(\theta) \left (\frac{\partial \psi}{\partial z} + 1 \right) \right]\
\end{align*}
$$

## Results and Discussion
