---
layout: post
title: Liquidのforループの中で降順の番号をつける方法
date: 2019-07-31 10:00:00 +0900
image: '/img/portfolio/4.jpg'
tags:
- jekyll
- markdown
introduction: Liquidのforループで業績一覧のようなものを作りたいときに、降順で番号をつけたかったのでそのメモ
categories: memo
---

タグ：{% for tag in page.tags %} {{ tag }}{% endfor %}

*2019年7月31日時点での情報なのでの私の理解なので、もっといい方法があったら更新します。*

---

## Introduction

Jekyll+Github Pagesで公開しているページのなかで、Liquidの `for` ループを使って業績一覧を作っていました。業績一覧といえば、最新の業績が一番上に来て、降順で並べるのが普通だと思います。それに伴って、番号も下から上に増えていって、最新の業績が何個目なのかを知ることができます。

目標としてはこんな感じです。

[3] 業績３つ目  
[2] 業績２つ目  
[1] 業績１つ目  

データとしてその業績が何個目なのかを入れておけば良いのだと思うのですが、業績の記載を忘れていたりして追加したときに、それ以降の番号を手動で修正しないといけなくなったらかなり面倒だと思います。

`for` ループもそうですが、Jelyllでは[Liquid](https://shopify.github.io/liquid/)が使えます。数を数えるくらいできそうなので実装してみようと思います。

---

## Methods and Results

### forループの復習

このブログの最新記事５つのタイトルを出力してみます。

**コード**

```
{% raw %}
{% for post in site.posts limit:5 %}
{{ post.title }}
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
```
{% raw %}
{% assign test_post_num = site.posts | size %}
{% for post in site.posts limit:5 %}
[{{ test_post_num | plus: test_dec_var }}] {{ post.title }}
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

```
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
