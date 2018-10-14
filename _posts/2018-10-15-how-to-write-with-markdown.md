---
layout: post
title: マークダウンの記述法
date: 2018-10-15 10:00:00 +0900
image: '/img/portfolio/4.jpg'
tags:
- jekyll
- markdown
introduction: 記事を投稿するときに使用するmarkdown形式の記述の仕方についてのメモ。
---

記事を投稿するときに使用するmarkdown形式の記述の仕方についてのメモ。

```ruby:qiita.rb
puts 'The best way to log and share programmers knowledge.'
```

```ruby:qiita&nbsp;motto.rb　(2)
puts 'The best way to log and share programmers knowledge.'
```

$$
\begin{align*}
\frac{\partial \theta}{\partial t}= \frac{\partial}{\partial z}
\left[ K(\theta) \left (\frac{\partial \psi}{\partial z} + 1 \right) \right]\
\end{align*}
$$

半径 $$ r $$ の円の面積は $$ \pi r^2 $$ であり、球の体積は $$ \frac{4}{3}\pi r^3  $$ である。

# 見出し1
## 見出し2
### 見出し3
#### 見出し4
##### 見出し5
###### 見出し6

ブロック改行  
段落1

段落2

Br改行
hoge
fuga(スペース2つ)  
piyo

> 引用  
> 引用
>> 多重引用

```
rint 'hoge'
```
~~~
print 'hoge'
~~~

これは `インラインコード`です。

    class Hoge
        def hoge
            print 'hoge'
        end
    end
    
class Hoge
    def hoge
        print 'hoge'
    end
end

hoge
***

hoge
___

hoge
---

~~テキスト~~

***

<font color="#089921">テキスト</font>

2x1

# My main heading
{: .intro }

This is my initial paragraph. In it I’d like to provide a link to the [Jekyll homepage](http://jekyllrb.com/ "Jekyll"). I want to add **bold** and *italic* formatting to text as well using the `strong` and `emphasis` tags.

This is another paragraph. I’d like to follow it with an unordered list.

* item 1
* item 2
* item 3

# Apply the class “main” to this heading
{: .main}

# Another heading with the ‘role’ attribute applied
{: role="banner"}

# This heading has two classes and one ID applied
{: .class1 .class2 #ID-1}

I want to wrap **this text** in a strong tag and *this text* in an emphasis tag.

I usually search using [Google](https://www.google.com "Google").

![My dog](/img/portfolio/4.jpg)

| Priority apples | Second priority | Third priority |
|-------|--------|---------|
| ambrosia | gala | red delicious |
| pink lady | jazz | macintosh |
| honeycrisp | granny smith | fuji |
