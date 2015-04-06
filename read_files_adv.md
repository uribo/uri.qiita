# webページやクラウド上にあるファイルを読み込みまくる ~ 応用編

-> [webページやクラウド上にあるファイルを読み込みまくる ~ 基礎編](http://qiita.com/uri/items/19159c7ff3f771cfa761) のつづき。

## Google Driveにあるspreadsheetを読み込む

最近公開されたほっとなパッケージ

[jennybc/googlesheets](https://github.com/jennybc/googlesheets)

このパッケージを使えば、GoogleDocsに保存しているファイルをR上で読み込んだり、新規のスプレッドシートを作成、編集できたりします。READMEにあるとおりですが、少しだけ使用方法を書いておきます。

```r
# devtools::install_github("jennybc/googlesheets")
library("googlesheets")
(my_sheets <- list_sheets()) # 実行するとファイルへのアクセスを許可するかどうかを尋ねるため、webブラウザが起動します。
# 許可すると、ログインしているGoogleアカウントに保存されたスプレッドシートのタイトルと個別のキーがずらずらと表示されます。
# Source: local data frame [39 x 10]
# 
#                       sheet_title                                    sheet_key       owner perm        last_updated version
# 1                      150406test 1AIjxNy5S_8ggEnXIlOJ8LwwCEtzKdt8NosEDFDoHipU   suika1127   rw 2015-04-06 12:28:15     new
### ...
```

ファイルの読み込みはやや複雑です。まず、`register_ss`関数に上のリストで出てきた`sheet_title`とそれに対応した`sheet_key`を渡渡すことでシートを読み込む準備を行います。シート名だけを渡した場合、キーが表示されるのでそれをあとで渡すことも可能です。

```r
register_ss(x = "150406test", key = "1AIjxNy5S_8ggEnXIlOJ8LwwCEtzKdt8NosEDFDoHipU") -> dat
```

Rで扱えるようなデータフレームにするためには`get_via_csv`関数を使います（`get_via_lf`関数というものもあるけど、違いがよくわからない）。

```r
get_via_csv(dat)
# Accessing worksheet titled "Sheet1"
# Source: local data frame [4 x 3]
# 
#      name score temp
# 1    taro     4   NA
# 2  hanako     3    2
# 3    mike     6   NA
# 4 musashi     8   NA
```

できました。

このパッケージのさらにすごいところは、新規のシートを作ったり、簡単な編集がR上でできること、そしてファイルのアップロードやダウンロードまでできてしまうことです。次の項目の説明のためにファイルをダウンロードします。

```{r}
download_ss("150406test", to = "~/Dropbox/share/150406download_test.csv")
# Downloading: 53 B     
# Sheet successfully downloaded: /Users/uri/Dropbox/share/150406download_test.csv
```

## Dropboxにあるテキストファイルを(ry

[karthik/rDrop2](https://github.com/karthik/rDrop2)

これまた最近公開されたライブラリ。これを紹介しておしまいです。

```{r}
# devtools::install_github('karthik/rDrop2')
library("rDrop2")
drop_auth() # 実行するとwebブラウザが立ち上がり、さきほどと同じくアクセス権の確認をおこないます
```

さきほどのパッケージでダウンロードしたファイルを読み込みましょう。

```
drop_read_csv(file = "share/150406download_test.csv")
name score temp
1    taro     4   NA
2  hanako     3    2
3    mike     6   NA
4 musashi     8   NA
```

gooooood!

つぎつぎと便利なライブラリが出てきて、追うのが大変ですね。

それでは Enjoy 前処理! 