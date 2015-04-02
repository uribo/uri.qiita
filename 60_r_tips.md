# R言語を扱う際のtips by Rstatistics.net

日本のR利用者の中であまり話題になっていないような気がしますが、[Rstatistics.net](http://rstatistics.net)が公開した"60 R Language Tips"というのが良い・自分のためになるので気になったところを紹介。

<blockquote class="twitter-tweet" lang="en"><p>60 Super Useful R Language Tips (and counting).. Free PDF Download! &#10;<a href="http://t.co/TdzJtYUj1X">http://t.co/TdzJtYUj1X</a> <a href="https://twitter.com/hashtag/rstats?src=hash">#rstats</a> <a href="https://twitter.com/hashtag/datascience?src=hash">#datascience</a> <a href="http://t.co/UT0oQTORX0">pic.twitter.com/UT0oQTORX0</a></p>&mdash; Learn R (@R_Programming) <a href="https://twitter.com/R_Programming/status/577867709058195457">March 17, 2015</a></blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

PDFが公開されているので、詳しくは原文をご覧ください。

## 1. 因子になった数値の変換には`as.numeric()`関数は使用しない

ときどきですが、数値であるはずのデータが要素データとされてしまうことがあります。その際、数値に変換する`as.numeric()`関数を使うと、値が変わってしまいます。

```r
c(1, 2.4, NA) %>% str()
# num [1:3] 1 2.4 NA
c("1", "2.4", "NA") %>% as.factor() %T>% str() -> tmp
# Factor w/ 3 levels "1","2.4","NA": 1 2 3
```

```r
as.numeric(tmp)
# [1] 1 2 3
```

これは`tmp`というベクターがカテゴリーデータであるため、水準の順番に数値を与えているために生じる問題です。

`as.character()`関数で一度文字列データに変換し、再度`as.numeric()`関数による変換をすることでこの問題を回避できます。

```r
as.character(tmp) %>% as.numeric()
# [1] 1.0 2.4  NA
```

今度はきちんと元の数値になりました。

## 11. セッション情報を表示する`sessionInfo()`関数

使用中のRのバージョンや使用したパッケージについて知りたいときに`sessionInfo()`関数が便利です。

```r
sessionInfo()
# R version 3.1.2 (2014-10-31)
# Platform: x86_64-apple-darwin13.4.0 (64-bit)
# 
# locale:
# [1] en_US.UTF-8/en_US.UTF-8/en_US.UTF-8/C/en_US.UTF-8/en_US.UTF-8
# 
# attached base packages:
# [1] graphics  grDevices utils     datasets  stats     methods   base     
# 
# other attached packages:
# [1] rmarkdown_0.5.1 devtools_1.7.0  ggplot2_1.0.1   magrittr_1.5    stringr_0.6.2   knitr_1.9      
# 
# loaded via a namespace (and not attached):
#  [1] colorspace_1.2-6 cowsay_0.2.9.999 digest_0.6.8     DYM_0.1          evaluate_0.5.5   formatR_1.1      fortunes_1.5-2 
#  [8] grid_3.1.2       gtable_0.1.2     htmltools_0.2.6  MASS_7.3-40      memoise_0.2.1    munsell_0.4.2    plyr_1.8.1     
# [15] proto_0.3-10     Rcpp_0.11.5      reshape2_1.4.1   RJSONIO_1.3-0    scales_0.2.4     tools_3.1.2    
```

リストで値が返ってくるので、各項目についてアクセスするにはこのように。

```r
sessionInfo()$R.version$version.string
# [1] "R version 3.1.2 (2014-10-31)"
```

また同様の機能は`devtools::session_info()`も備えています。さらに似たような機能ですがtips 54でも紹介されています。

## 34. 複数パッケージの読み込みを一行で

通常、パッケージの読み込み（`require()`あるいは`library()`）で指定できるパッケージの数は一つですが、次のようにすると複数のパッケージを一度に読み込むことが可能です。

```r
lapply(c("ggplot2", "gridExtra"), require, character.only = TRUE)
```

## 56. パッケージの情報や関数を一覧表示させる

関数のヘルプを表示するには`?関数名`あるいは`help(関数名)`ですが、パッケージ全体の関数について知りたいときなどに便利なtips

```r
library(help = ggplot2)
```

`library()`関数の引数helpに情報を得たいパッケージ名を与えることで各種情報や関数が表示されます。

Enjoy!
