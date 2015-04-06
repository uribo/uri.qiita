# webページやクラウド上にあるファイルを読み込みまくる ~ 基礎編

R本の著者の多くは、サポートとしてスクリプトや使用するデータをwebページで公開してくれています。Rには、これらのファイルを保存せずに読み込む機能やパッケージが備わっています。ちょっと調べてみたので今回は「基礎編」と「応用編」の２つに分けてその方法を紹介したいと思います。基礎編では標準関数と最も標準だと思われる方法をとります。応用編では、いわゆるクラウドにあるファイル（GoogleDocs, Dropbox）にあるファイルを読み込む方法について述べます。

-> [webページやクラウド上にあるファイルを読み込みまくる ~ 応用編]()

## Webページにアップロードされているテキストファイルを読み込む

ものによっては、そのまま`read.csv`で読み込めるファイルもあります。今回は緑本の久保さんが公開している[本のサポートページ](http://hosho.ees.hokudai.ac.jp/~kubo/ce/IwanamiBook.html)から、プログラムに使うCSVファイルをとってきます。

```r
dat <- read.csv("http://hosho.ees.hokudai.ac.jp/~kubo/stat/iwanamibook/fig/poisson/data3a.csv")
str(dat)
# 'data.frame':	100 obs. of  3 variables:
#  $ y: int  6 6 6 12 10 4 9 9 9 11 ...
#  $ x: num  8.31 9.44 9.5 9.07 10.16 ...
#  $ f: Factor w/ 2 levels "C","T": 1 1 1 1 1 1 1 1 1 1 ...
```

できました。

上記の方法で読み込めないファイルは`RCurl`パッケージの`getURL`関数をかませることで読み込めたりします。

> もちべーじょん... Appendixとして使用したデータを付けている論文、とてもありがたい。けど、いちいちダウンロードしているのも面倒かつファイルの置き場に困るので使い捨てな感じにしたい。

```r
library("RCurl")
url <- getURL("http://datadryad.org/bitstream/handle/10255/dryad.77075/Thomas_etal_2014_Dryad.txt?sequence=1")
dat <- read.table(text = url, header = TRUE)
# 結果は省略します
```

### GitHubにあるテキストファイルを読み込む

GitHubにCSVを置いておけば、みなさん気楽に遊べますよね。今回はおなじみの「歩数」データをかっさらってきます。

```r
url <- getURL("https://raw.githubusercontent.com/dichika/mydata/master/ore.csv")
dat <- read.csv(text = url, header = TRUE)
head(dat)
#         time data
# 1 2015-01-03 7754
# 2 2015-01-04    0
# 3 2015-01-05 9096
### 以下省略
```

## webページのテーブルからデータを取得する

### XML::readHTMLTableを使う方法

これは「[R for Everyone](http://www.jaredlander.com/r-for-everyone/)」（新しくて良書）に掲載されていたtipsです。

```r
readHTMLTable("http://www.jaredlander.com/2012/02/another-kind-of-super-bowl-pool/")
# $`NULL`
#                V1      V2        V3
# 1   Participant 1 Giant A Patriot Q
# 2   Participant 2 Giant B Patriot R
# 3   Participant 3 Giant C Patriot S
### 以下省略
```

```r
getURL("https://github.com/uribo/Japan.useR/blob/master/README.md") %>% readHTMLTable(header = TRUE, stringsAsFactors = FALSE)
# $`NULL`
#                       Name              Organizer                Place
# 1                Fukuoka.R             @nonki1974     Fukuoka, Fukuoka
# 2  HiRoshima.R (HijiyamaR)                @sakaue Hiroshima, Hiroshima
# 3                Kashiwa.R            @Acafe_info       Kashiwa, Chiba
### 以下省略
```

## rvestを使う方法

[rvest: easy web scraping with R | RStudio Blog](http://blog.rstudio.org/2014/11/24/rvest-easy-web-scraping-with-r/)にあるとおりです。

## Javascriptベースのwebページからデータを抽出する方法

[Short R tutorial: Scraping Javascript Generated Data with R](http://blog.datacamp.com/scraping-javascript-generated-data-with-r/)にあるとおり。

最後のほうは疲れてしまいました。時間があれば最後の方法は説明できれば良いなと思います。
そして次からが真打ちです（つづく）。