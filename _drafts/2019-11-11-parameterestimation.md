---
layout: post
title: BrdUラベリングの時系列データからパラメータ推定
date: 2019-11-11 10:00:00 +0900
image: '/img/portfolio/4.jpg'
tags:
- research
- R
description: ウイルス感染と常微分方程式 (シリーズ・現象を解明する数学)の中で紹介されている、BrdUラベリングデータから常微分方程式で記述された数理モデルのパラメータを推定する方法
categories: labwebsite first
---

## Introduction

岩見真吾他（箸）のウイルス感染と常微分方程式 (シリーズ・現象を解明する数学)を元に時系列データから数理モデルのパラメータを推定する方法を解説する。

ウイルス感染と常微分方程式 (シリーズ・現象を解明する数学)  
[https://amzn.to/2JOWl5P](https://amzn.to/2JOWl5P)

Rを使った最小二乗法によるデータフィッティングの方法に重点を置き、数理モデルの説明は最小限にする。

使用するデータは、岩見真吾, 佐藤佳, 竹内康博 (2017). 「ウイルス感染と常微分方程式」. 共立出版



---

## Methods and Results

### forループの復習

このブログの最新記事５つのタイトルを出力してみます。

**コード**

```html
{% raw %}
{% for post in site.posts limit:5 %}
<p>{{ post.title }}</p>
{% endfor %}
{% endraw %}
```

<br>
**結果**

> {% for post in site.posts limit:5 %}
> {{ post.title }}  
> {% endfor %}

`for post in site.post` では日付の新しい順に記事を取ってきます（ `limits:5` は初めの５つに限定するためのフィルタです。）。

このforループの中で全記事中の何番目なのかを示すために以下のようにします。

**コード**
```html
{% raw %}
{% assign test_post_num = site.posts | size %}
{% for post in site.posts limit:5 %}
<p>[{{ test_post_num | plus: test_dec_var }}] {{ post.title }}</p>
<div style="display: none">{% decrement test_dec_var %}</div>
{% endfor %}
{% endraw %}
```

**結果**

> {% assign test_post_num = site.posts | size %}
> {% for post in site.posts limit:5 %}
> [{{ test_post_num | plus: test_dec_var }}] {{ post.title }}
> <div style="display: none">{% decrement test_dec_var %}</div>
> {% endfor %}

一行目の{% raw %} `{% assign test_post_num = site.posts | size %}` {% endraw %}で `test_post_num` に総記事数を入れています。

{% raw %} `{% decrement test_dec_var %}` {% endraw %}は読まれるたびに１ずつ減っていきます。読まれるたびに出力されるので `<div>` タグで囲って `style="display: none"` として見えないようにしています。

```html
{% raw %}
{{ test_dec_var2  }}
{% decrement test_dec_var2 %}
{% decrement test_dec_var2 %}
{% decrement test_dec_var2 %}
{% endraw %}
```
> {{ test_dec_var2  }}  
> {% decrement test_dec_var2 %}  
> {% decrement test_dec_var2 %}  
> {% decrement test_dec_var2 %}  

`{% raw %}{{ test_post_num | plus: test_dec_var }}{% endraw %}`とすることで、総記事数に１ずつ減っていく数を足して、降順に減る番号を実装しました。

<hr>

## Discussion

`decrement` では最初に現れたときに `-1` になるので、forループの最後で更新するようにしています。また、ループの最初は何も入っていないのですが、 `plus: ` としても問題はありませんでした。

この方法だと、ループごとに使う変数を管理する必要があるので、間違えて被ってしまったときに変な数字が出てしまうと思います。また、 `style="display: none"` となっていて、生成されるhtmlファイルもみにくくなります。もう少し管理の楽な方法で実装したいです。
