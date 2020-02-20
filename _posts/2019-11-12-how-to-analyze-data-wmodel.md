---
layout: page
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

{% for  post in site.categories.research %}

{% include card.html url=post.url image=post.image title=post.title description=post.description last_modified_at=post.last_modified_at date=post.date %}

{% endfor %}
