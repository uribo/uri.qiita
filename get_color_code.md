# ファイル中で指定しているカラーコードを把握する #進捗を支える技術

どうもシリアルパッケージクリエイター見習いです。

呪文のような**カラーコード（`#000000`, `#FFFFFF`の違いすら曖昧）を覚えることができない**ので、ファイルを見返してカラーコードを確認することがあります。しかし、そんなこともいちいちやっていると面倒なので、簡単にファイル中のカラーコードを把握したい、というもの。

## color_picker: そんな関数

> より正確にカラーコードを取得するよう、なおかつコードの可読性を高めるために@hoxo_mさんがコメントしてくれました。感謝。

```r
# 関数の定義
color_picker <- function(file, show = TRUE, ...) {
  col <- readLines(file, warn = FALSE) %>%
  stringr::str_match_all("[\"\'](#[0-9a-fA-F]{6})[\"\']") %>% 
  Filter(function(x) length(x) != 0, .) %>%
  Map(function(x) x[,2], .) %>% 
  unlist %>%
  unique %>%
  print
  
  if(show == TRUE) {
    colortools::pizza(col)
    } else {
      NA
    print(col)
    }
}
```

要 `magrittr`, `stringr`, `colortools`

```r
# 使い方
# test.Rというファイル内で指定されているカラーコードを返します
# show = TRUEにするとpizzaができあがります（笑
color_picker("test.R", show = FALSE)
# [1] "#000000" "#FFFFFF" "#9E9E9E" "#87CEEB" "#32CD32"
```

**色名とかは無理**。シャープではじまるカラーコードにのみ対応。上手くいかないこともあるから気をつけてください...。

`colortools`パッケージの`pizza関数`を使わせてもらって、プロットもしちゃいます。pizzaの代案としては`popbio`パッケージの`colorguide関数`がありましたが、そこはお好みで。

## 宣伝

まだ全然機能がないですが、R使いのためのデザインツールパッケージ（[uribo/designer](https://github.com/uribo/designer)）を開発中です...

```r
devtools::install_github("uribo/designer")
```

**男の価値は作ったパッケージの数で決まる**、ということなのでじゃんじゃん~~無駄な~~パッケージを作っていきたい所存です。