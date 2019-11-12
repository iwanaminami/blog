---
layout: post
title: 数理モデルと時系列データの解析
date: 2019-11-12 10:00:00 +0900
image: '/img/covers/brduestimation.png'
tags:
- research
- R
- data analysis
- parameter estimation
description: 時系列データから数理モデルのパラメータを推定するのに必要な技術・知識をまとめます。
categories: research
permalink: /research/dataanalysis/
---

{{ page.description }}

---

## BrdUラベリングデータとターンオーバーの推定


{% for  post in site.tags.BrdU %}
### [- {{ post.title }}]({{ post.url }})

{{ post.description }}  
**更新日：{{ post.last_modified_at | date: "%Y年%m月%d日" }}** | {{ post.date | date: "投稿日：%Y年%m月%d日" }}  
[[more]]({{post.url}})

{% endfor %}
