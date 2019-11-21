---
layout: post
title: Rでの時系列データの準備
date: 2019-11-12 10:00:00 +0900
last_modified_at: 2019-11-12 17:00:00 +0900
image: '/img/covers/brduestimation.png'
tags:
- research
- R
- parameter estimation
- BrdU
description: Rで時系列データを解析に使うための準備や読み込みの方法、データ形式などについてまとめています。
categories: research
---

---


## Introduction

時系列データを解析するには、まず、実験データを読み込んで扱いやすい形式にして、変数に保存する必要がある。コードの中に直接データを入力しても良いが、数が多くなると面倒であるし、他の解析で利用するための使い回しが不便である（誤植してしまうかもしれない）。データはある決まったファイルに保存し、解析のたびに読み込むようにすると間違いが少なくなり、コードを確認する手間も省くことができる。

主要なプログラミング言語はテキストデータの読み込み（と書き込み）をサポートしており、Rはデータの整理・保存に使用するようなExcelファイル・csvファイルにも対応しているので、表形式で編集して読み込むということも可能である。

このページでは、テキストデータを作り、ある程度成形した上で読み込む方法をまとめる。複数の測定項目について時系列データを取得している場合に有効であると考えられる。※主流ではないし、他にもいろいろな方法が考えられる。

---

## Materials and Methods

### 想定するデータ

ここでは、以下のような３種類の血中マーカーを扱うことを考える。

データ

| Days | 1 | 2 | 3 | 4 | 5 |
|------|---|---|---|---|---|
| Protein A | 2 | 3 | 4 | 6 | 5 |
| Protein B | 2 | 3 | 4 | 6 | 5 |
| Protein C | 2 | 3 | 4 | 6 | 5 |

### data.frameでデータの準備

data.frameの詳細についてはDocumentationや日本語で解説してあるページを参照

[data\.frame function \| R Documentation](https://www.rdocumentation.org/packages/base/versions/3.6.1/topics/data.frame)

[R\-Source](http://cse.naro.affrc.go.jp/takezawa/r-tips/r/39.html)

```R
data.frame(x=c(1,2,3),y=c("mouse1","mouse2","mouse3"))
```
とすれば、`x`という要素に`1,2,3`というデータ、`y`にはそれに対応する`mouse1, mouse2, mouse3`というマウスのid的なものが入る。  


---

## Results and Discussion
