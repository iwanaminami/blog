---
layout: post
title: google driveのファイルを埋め込む
date: 2020-05-19 12:00:00 +0900
last_modified_at: 2020-05-19 12:00:00 +0900
image:
tags:
- GoogleDrive
description: Google Driveに保存したベクターファイルを埋め込みたい
categories: test
---

## どこかで使える画像集

個人・商用問わずある程度自由に使ってください。

### 作品等の一部として、もしくは部分的に改変して利用する場合

- クレジットの表記の必要はありません。
- 営利目的で利用できます。
- 自由に改変できます。

### 元の形式のまま利用する場合

- 元の形式での営利目的での利用、二次配布する場合は、このサイトへのリンクを明記してください。

このサイトのURL: url

eps埋め込み

<iframe src="https://drive.google.com/file/d/1gERYfaT5a8FyfwkXFMc0bEUaplgZu3fV/preview" width="640" height="480"></iframe>

png埋め込み

<iframe src="https://drive.google.com/file/d/1M0l2aLSLG7XTi-QXwxei7cKurwDJDoFP/preview" width="640" height="480"></iframe>


[pngダウンロード](https://drive.google.com/uc?export=download&id=1M0l2aLSLG7XTi-QXwxei7cKurwDJDoFP)



## メモ

iframeでプレビュー

```html
<iframe src="https://drive.google.com/file/d/<id>/preview" width="640" height="480"></iframe>
```

ダウンロード用

```md
[pngダウンロード](https://drive.google.com/uc?export=download&id=<id>)
```

### ファイル形式

アウトラインを作成すべし！

イラレなど → EPS

パワーポイントなど → SVG

画像 → PNG
