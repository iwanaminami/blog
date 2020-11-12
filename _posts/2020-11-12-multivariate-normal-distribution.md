---
layout: post
title: 【R tips】多次元正規分布から乱数を生成する
date: 2020-11-12 12:00:00 +0900
last_modified_at: 2020-11-12 12:00:00 +0900
image:
tags:
- R
- research
description: 多次元正規分布から乱数を生成しようと思ったけど、複数の正規分布と多次元正規分布は違うらしい。
categories: research
---

## 多次元正規分布

[多変量正規分布 \- Wikipedia](https://ja.wikipedia.org/wiki/%E5%A4%9A%E5%A4%89%E9%87%8F%E6%AD%A3%E8%A6%8F%E5%88%86%E5%B8%83)

「多変量正規分布に従う確率変数ベクトルの相異なる2成分は独立であるとは限らない。」らしい。

そして、「正規分布に従う確率変数の対は、必ずしも2変量正規分布には従わない」らしい。

えっ、、。独立な正規分布に従う複数の確率変数があったとしても多次元正規分布とは別ものですか？

確認してみる。

## Rで正規分布に従う乱数の生成

とりあえず正規分布に従う乱数を生成してみる。

```R
## あとで使う
> n_sample <- 10000
> par_mu <- c(a = 1, b = 2, c = 3, d = 4)
> par_sigma <- diag(length(par_mu))

## 生成
> norm_sampled <- c()
> for(i in 1:length(par_mu)){
+   norm_sampled <- cbind(norm_sampled, rnorm(n = n_sample, mean = par_mu[i], sd = par_sigma[i, i]))
+ }

> head(norm_sampled)
            [,1]      [,2]     [,3]     [,4]
[1,]  0.02048599 3.2279251 3.312449 3.587667
[2,]  3.22529915 3.0694514 1.407773 4.675620
[3,] -0.42455852 3.4634128 1.064422 1.575292
[4,] -0.17052506 3.1231589 3.066041 3.736053
[5,]  0.24281165 1.2057380 1.973545 4.391110
[6,] -0.44881602 0.5109505 4.470853 3.165442
```

４パターン生成してみた。

## Rで多次元正規分布に従う乱数の生成

package`MASS`に多次元正規分布に従う乱数を生成する関数があるらしい。
```R
library(MASS)
```

`mvrnorm()`という関数を使う。引数は生成する乱数の数`n`、平均のベクトル`mu`、分散共分散行列`Sigma`。
```R
n_sample <- 10000 #10000
par_mu <- c(1, 2, 3, 4) #平均のベクトル
par_sigma <- diag(length(par_mu)) #分散共分散行列

mvnorm_sampled <- mvrnorm(n = n_sample, mu = par_mu, Sigma = par_sigma)
```

`mvrnorm()`の戻り値はmatrixぽい。
```R
> head(mvnorm_sampled)
          [,1]     [,2]     [,3]     [,4]
[1,] -1.434757 1.495079 1.689496 3.524325
[2,]  2.791495 1.065469 2.496554 6.569992
[3,]  2.811157 1.526129 1.964177 5.520057
[4,] -0.156930 2.509537 1.169475 3.918754
[5,]  3.520579 1.546526 3.545443 4.338753
[6,]  1.383880 1.826391 2.873288 3.731838

> dim(mvnorm_sampled)
[1] 100   4
```

平均のベクトルを名前付きにしたら`mvrnorm()`から帰ってくるmatrixの列名がつく。
```R
> par_mu <- c(a = 1, b = 2, c = 3, d = 4)
> mvnorm_sampled <- mvrnorm(n = n_sample, mu = par_mu, Sigma = par_sigma)
> head(mvnorm_sampled)
              a        b        c        d
[1,] -0.1046164 2.674349 4.308218 3.181429
[2,]  1.2705906 1.102443 2.139671 6.446919
[3,]  1.5674845 1.441965 1.049699 3.295079
[4,]  0.8991505 3.320809 1.917985 4.290551
[5,]  2.1401209 1.801722 2.244247 3.085911
[6,]  0.4790264 1.857652 4.421825 4.670735
```

## 重ねてみる

```R
> library(ggplot2)
> ds <- data.frame(x = c(norm_sampled[, 1], mvnorm_sampled[, 1]), label = rep(letters[1:2], each = n_sample))
> plt <- ggplot(data = ds, aes(x = x, color = label, fill = label)) +
+   geom_histogram() +
+   scale_color_manual(values = c("#000000", "#ff0000"), label = c("Normal dist", "Multivariate normal dist")) +
+   scale_fill_manual(values = c("#00000040", "#ff000040"), label = c("Normal dist", "Multivariate normal dist")) +
+   theme_classic()
> ggsave(plt, filename = "../outputs/hist_test.png", width = 10, height = 5)
```

![](/img/20201112/hist_test.png)

同じっぽい？
