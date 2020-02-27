---
layout: post
title: 【R tips】Rのlm()を使った線形回帰のまとめ
date: 2020-02-27 12:00:00 +0900
last_modified_at: 2020-02-27 12:00:00 +0900
image:
tags:
- research
- R
- parameter estimation
description: 線形回帰をするときに必要な結果を取得する方法をメモ。線形回帰をある程度自動でやってくれるのはいいのだけれど、何をやっているかを理解しておかないといけない。
categories: research
---

---

保存用

---

### 係数の信頼区間

```R
> confint(result, level = 0.95)
```

推定値と標準誤差からの計算も

[Rの簡単な手引き６](https://www.econ.hokudai.ac.jp/~kakizawa/R/R_6.html)
