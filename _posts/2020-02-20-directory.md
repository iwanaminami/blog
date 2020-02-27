---
layout: post
title: 【R tips】相対パス、ルートパス、ホームディレクトリなど
date: 2020-02-20 03:00:00 +0900
last_modified_at: 2020-02-20 03:00:00 +0900
image: 
tags:
- research
- R
description: プログラミングをする上で必要なパス、ディレクトリの基本です。
categories: research
---

---


## Introduction

プログラミングをする上で、読み込み・書き込みをするときにファイルやディレクトリを指定することがあります。ファイルのある場所やファイルを作成する場所を指定することです。いくつか指定方法があるのでまとめます。

---

## ディレクトリ

フォルダと呼ばれるものです。ファイルを格納する場所を示します。

## ルートパス

ルートパスとは、コンピュータの中でそのファイルの住所を示します。通常扱うファイルのルートパスは次のようになります。

Macの場合
```
/Users/_username_/_directory_/.../_filename_.extension
```

このとき最初の`/`はルートディレクトリを表していて、通常FinderではMacintosh HDと表示されます。  
Macの場合、`/Users/_username_/`のディレクトリはそのユーザのホームディレクトリと呼ばれ、`~`で表すことができます。  
以下は上のパスと同じです。
```
~/_directory_/.../_filename_.extension
```


Windowsの場合
```
C:\Users\_username_\Documents\...\_filename_.extension
```

`C:\`はCドライブとして設定されたディスクを示していて、ルートディレクトリです。

## Rでのworking directory

Rでは`setwd()`を使ってworking directoryを設定できます。working directoryを設定すると、相対パスを指定することでファイルの扱いが楽になることがなります。現在のworking directoryは`getwd()`で見ることができます。

```R
> setwd('~/Desktop')
> getwd()
[1] "/Users/_username_/Desktop"
```

## 相対パス

Rで相対パスとはworking directoryからの相対的なパスのことです。例えばworking directoryが`"~/Desktop"`であるとき、デスクトップにおいている`"file.R"`というファイルのルートパスは`"~/Desktop/file.R"`ですが、`"file.R"`でアクセスできます。

```R
> getwd()
[1] "/Users/_username_/Desktop"
> source("file.R")
```

また、working directoryから一つ上の階層のディレクトリは`"../"`で表され、working directoryは`"./"`で表されます。Macではデスクトップフォルダ（Desktop）も書類フォルダ（Documents）もホームディレクトリ（~）の直下にありますが、以下のようにすれば書類（Documents）のディレクトリにあるファイルにアクセスできます。

```R
> getwd()
[1] "/Users/_username_/Desktop"
> source("../Documents/file.R")
```

## Rでの書き出しのコツ

Rではsave()などを使ってデータやグラフをファイルとして保存することができます。

例えば`save(data, "data.txt")`とすればworking directoryに`"data.txt"`が作成されます。多くのファイルを書き出して、ソースファイルと書き出したファイルを混ぜたくない場合は、working directoryの直下に`"outputs"`のようなディレクトリを作成しておいて、`save(data, "./outputs/data.txt")`としてあげればファイルを整理することができます。
