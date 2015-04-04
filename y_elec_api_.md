# RでAPIデータを扱うときはrlistを使うとストレスフリー

こんな話があって、[Yahoo提供の電力使用状況APIで遊ぶ - Qiita](http://qiita.com/Gen6/items/1d17d0af1cf7dfb3abbd)、[こんな記事](http://rpubs.com/uri-sy/yahoo_latest_power_usage_api)を書いた。のだけども、リストの操作に慣れていないせいもあってかなんか汚い。

というわけでR上でのリストオブジェクトの扱いをよしなにしてくれる[`rlist`](http://cran.r-project.org/web/packages/rlist/index.html)パッケージに触れてみた。

**結論: `rlist`べんり・しゅごい。**
  
`rlist`、いろいろ関数あって複雑だけど、基本的なところだけでも抑えておけば神に近づける気がする
  
というわけで上記のrpubs記事と同じことを`rlist`を使ってやってみる。

```r
# 使用するパッケージ
library("rlist")
library("dplyr")
```

```r
api.key <- APIキー
area <- c("hokkaido", "tohoku", "tokyo", "chubu", "kansai", "kyushu")

url <- paste("http://setsuden.yahooapis.jp/v1/Setsuden/latestPowerUsage?appid=", api.key, "&area=%s&output=json", sep = "") %>%
  sprintf(area) %>% 
  list.load("json") %>% 
  list.ungroup() # このへんがみそ
```

```r
str(url) # ↓値は省略する
# List of 6
# $ ElectricPowerUsage:List of 5
# ..$ Area    : chr "hokkaido"
# ...
# $ ElectricPowerUsage:List of 5
# ..$ Area    : chr "tohoku"
# ... 以下略
```

`rlist`にある関数ではAPIにあるパラメータ名を直接扱えるのでストレスが軽減する。パラメータ名を知りたいときは

```r
list.names(url$ElectricPowerUsage)
# [1] "Area"     "Usage"    "Capacity" "Date"     "Hour"    
```

要素を確認

```r
list.table(url, Area)
# Area
# chubu hokkaido   kansai   kyushu   tohoku    tokyo 
# 1        1        1        1        1        1
```

各電力会社のデータはurl[[i]]に格納されており、次はこのリストから`list.mapv`関数を使って値を取り出す。例によって、数値が文字列になっているので`transform`関数で型変換。使用量 / 供給量の割合の`usage.pct`という列を新たに追加して、`res`というデータフレームを作成。

```r
cbind(area,
      usage    = list.mapv(url, Usage$`$`, use.names = FALSE), 
      capacity = list.mapv(url, Capacity$`$`, use.names = FALSE)) %>% 
  as.data.frame() %>% 
  transform(usage    = as.numeric(as.character(usage)),
            capacity = as.numeric(as.character(capacity))) %>% 
  dplyr::mutate(usage.pct = usage / capacity * 100) -> res
```

可視化はrpubsと同じなので省略。水準を入れ替えたいときは`res$area <- area %>% factor(area)`を忘れずに。

## 参考

* [Introduction | rlist Tutorial](http://renkun.me/rlist-tutorial/)
* [r - How to convert a data frame column to numeric type? - Stack Overflow](http://stackoverflow.com/questions/2288485/how-to-convert-a-data-frame-column-to-numeric-type)
