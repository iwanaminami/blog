---
layout: post
title: 【R tips】ggplot2でラベルを好きな順番に並べる方法
date: 2020-02-17 03:00:00 +0900
last_modified_at: 2020-02-17 03:00:00 +0900
image: '/img/portfolio/1.png'
tags:
- research
- R
- ggplot2
description: ggplot2で色分けなどにつかったラベルをレジェンドに表示すると文字順にソートされるので、これを回避する方法。
categories: research
---

---


## Introduction

ggplot2で色分けなどにつかったラベルをレジェンドに表示すると文字順にソートされるので、これを回避する方法。

---

## 解決策

データフレームを作る

```R
> test <- data.frame(x=rnorm(10), label = c(rep("b",5),rep("a",5)))
> test
            x label
1   0.2221520     b
2   1.2009898     b
3   0.6672509     b
4   1.9525818     b
5   0.5154996     b
6   0.2365778     a
7  -1.9792533     a
8  -0.3790092     a
9   1.6983747     a
10  1.2131910     a
>
```

データフレームを作る際に文字列を含むベクトルを要素にすると、その列はfactor型になる。

```R
> is.factor(test$label)
[1] TRUE
> is.factor(test$x)
[1] FALSE
```

Labelsは自動で文字の順番にソートされる。

```R
> levels(test$label)
[1] "a" "b"
```

この状態でグラフをかくとレジェンドのラベルの順番は自動でソートされた順番になる。

```R
> plt_test <- ggplot(data=test, aes(x=x, color=label)) +
    geom_histogram()
> ggsave(plot = plt_test, filename = "test.png")
```

![](/img/20200217/test.png)

これを```"b","a"```の順番にしたい場合には、データフレームを作るときに```factor()```で```levels```を指定しておけば良い。

```R
> test2 <- data.frame(x=rnorm(10), label = factor(c(rep("b",5),rep("a",5)),levels = c("b","a")))
> test2
             x label
1  -1.22230476     b
2   0.09763175     b
3   0.07651087     b
4  -2.37786336     b
5   0.38975093     b
6   0.09128582     a
7  -0.40383193     a
8  -0.43032947     a
9   1.13458979     a
10  1.69728098     a
> levels(test2$label)
[1] "b" "a"
```

このデータフレームを使えばグラフのラベルのレジェンドの順番も```"b","a"```になる。

```R
> plt_test2 <- ggplot(data=test2, aes(x=x, color=label)) +
    geom_histogram()
> ggsave(plot = plt_test2, filename = "test2.png")
```

![](/img/20200217/test2.png)
