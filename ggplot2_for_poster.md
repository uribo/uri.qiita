# 学会発表のためのggplot2の設定めも

気がつけばもう何ヶ月も前の話ですが、学会発表のためにポスターに使う図の設定に戸惑ったのでめもです。なお**作図ファイルの形式はpdf**で、R Markdownによる自動作図です（png形式だとサイズを変更する際に粗くなってしまうので）。ここに貼り付けている画像はPDFをpng形式に変換したものです。

完成形はこんな感じ。

![poster のコピー.png](https://qiita-image-store.s3.amazonaws.com/0/19462/dcba409f-e614-398c-8481-1842c0d314b8.png)

[GitHubリポジトリ](https://github.com/uribo/poster_150319ESJ62Kagoshima)にPDFファイルがありますので興味があればどうぞ。これからの作図はirisデータでやっていますが、データが違うだけでやった方法は同じです。

-----

まず、通常の`ggplot2`でのプロットを見てみましょう。このままでも良いのですが、`ggplot2`は各種の変更も簡単なので、好みの図となるようにあれこれ変えていきます。

```r
library(ggplot2)
p <- ggplot(data = iris, aes(x = Sepal.Length, y = Petal.Length)) + 
  geom_point(aes(colour = Species))
plot(p)
```

![default-1.png](https://qiita-image-store.s3.amazonaws.com/0/19462/54e28aa3-165c-6523-9843-faa0f8d505d4.png)

## テーマを変更する

全体の見た目はテーマを設定しなおすことで変更が可能です。`ggplot2`のテーマRで`?ggtheme`とするか、[こちらのページ](http://docs.ggplot2.org/dev/vignettes/themes.html)を参考ください。あるいは、別のテーマ用パッケージ（[cttobin/ggthemr](https://github.com/cttobin/ggthemr)）を読み込んで変更もできます。

今回は白地の背景にx,y両軸の補助線をかかない`theme_classic`を使いました。

```r
p + theme_classic()
```

とすれば適用されますが、個々の図ではなくRセッション中の設定としてこちらのテーマを適用するように、`theme_set`関数で`theme_classic`の設定を適用させておきます。

```r
theme_set(theme_classic(base_size = 18, base_family = "Helvetica"))
```

![set_theme-1.png](https://qiita-image-store.s3.amazonaws.com/0/19462/a08e1838-beda-36fd-2789-0f743117dde3.png)


ベースとなるフォントの種類、サイズもここで指定します。こうしておけば、Rのセッションが終了するまでこの設定を保つことができます。

## 軸ラベルに日本語を使う

`theme`関数にてフォントファミリーを細かく設定できます。ここでは游ゴシック（YuGo-Medium）を使いました。

```r
theme_set(theme_classic(base_size = 36, base_family = "YuGo"))
quartzFonts(YuGo = quartzFont(rep("YuGo-Medium", 4)))
p + 
  scale_x_continuous(name = "萼片長", breaks = seq(0, 10, 2)) + 
  scale_y_continuous(name = "花弁長", breaks = seq(0, 8, 4)) +
  theme(text = element_text(family = "YuGo-Medium"),
        axis.title = element_text(size = 36),
        axis.text.x = element_text(family = "Helvetica", size = 28),
        axis.text.y = element_text(family = "Helvetica", size = 28))
```

![jp_label-1.png](https://qiita-image-store.s3.amazonaws.com/0/19462/3f33a5b6-2c55-14a2-5e0d-b3b3d3c3ca64.png)


### 軸ラベルの改行

図の幅よりラベルが長いと不格好なので適当に改行します。`\n`が改行するコマンドなので、ラベル中に付け加えます。

```r
p +
  scale_x_continuous(name = "がくへんちょう\n（せんちめーとる）", breaks = seq(0, 10, 2)) + 
  scale_y_continuous(name = "かべんちょう\n（せんちめーとる）", breaks = seq(0, 8, 4)) +
  theme(text = element_text(family = "YuGo-Medium"),
        axis.title = element_text(size = 36),
        axis.text.x = element_text(family = "Helvetica", size = 28),
        axis.text.y = element_text(family = "Helvetica", size = 28))
```

![jp_label2-1.png](https://qiita-image-store.s3.amazonaws.com/0/19462/e28989d7-4cc0-a53b-5eb9-024d36474462.png)


## 枠を透過させる

ポスターが青とか緑とか、何かの色で塗りつぶしてある背景だと、プロットした図を配置した際にちょっとダサい。というわけで透過させます。pngなら透過も簡単ですが、pdfの図を貼り付けるので少し工夫します。

```r
p +
  scale_x_continuous(name = "がくへんちょう\n（せんちめーとる）", breaks = seq(0, 10, 2)) + 
  scale_y_continuous(name = "かべんちょう\n（せんちめーとる）", breaks = seq(0, 8, 4)) +
  theme(text = element_text(family = "YuGo-Medium"),
        axis.title = element_text(size = 36),
        axis.text.x = element_text(family = "Helvetica", size = 28),
        axis.text.y = element_text(family = "Helvetica", size = 28),
        plot.background = element_rect(fill = "#87CEEB10"))
```

`theme`関数の引数`plot.background`に`element_rect`（データの各点などが図示される領域）の背景色を青（`#87CEEB`）の10%透過を指定しました。ポスターの背景色と合わせると良い感じになります。

![opacity-1.png](https://qiita-image-store.s3.amazonaws.com/0/19462/34b412e9-d61b-74db-bc0d-f4ff1b1ba6de.png)


## 複数の図を一つにまとめる

`gridExtra`パッケージを使います

```r
library(gridExtra)

p1 <- ggplot(data = iris, aes(x = Sepal.Length, y = Petal.Length)) +
  geom_point(size = 6, aes(colour = Species)) + 
  scale_x_continuous("萼片長", breaks = seq(0, 10, 2)) + 
  scale_y_continuous("花弁長", breaks = seq(0, 8, 4))
  
p2 <- ggplot(data = iris, aes(x = Sepal.Length, y = Petal.Length)) +
  geom_point(size = 6, aes(colour = Species)) + 
  scale_x_continuous("萼片長", breaks = seq(0, 10, 2)) + 
  scale_y_continuous("花弁長", breaks = seq(0, 8, 4))

grid.arrange(p1, p2, ncol = 2)
```

![multiple_plot-1.png](https://qiita-image-store.s3.amazonaws.com/0/19462/3fcb69c9-0c2c-2cfc-5518-31d670723594.png)

## 数式を埋め込む

あとで書く。ほかにもtipsがあった気がするけど忘れてしまいました...思い出したら書きます。

## 参考

* H.ウィッカム著（石田基広・石田和枝訳）. 2012. グラフィックスのためのRプログラミング ggplot2入門. *丸善出版*.
* Winston Chang. 2012. R Graphics Cookbook: Practical Recipes for Visualizing Data. *O'Reilly*.
* [Beautiful plotting in R: A ggplot2 cheatsheet | Technical Tidbits From Spatial Analysis & Data Science](http://zevross.com/blog/2014/08/04/beautiful-plotting-in-r-a-ggplot2-cheatsheet-3/)
* [Using CJK Fonts in R and ggplot2 | Hi!!](https://kohske.wordpress.com/2011/02/26/using-cjk-fonts-in-r-and-ggplot2/)
* [ggplot2 themes](http://docs.ggplot2.org/dev/vignettes/themes.html)
* [ggplot2で論文用の図を作るときに使いたいオプション（点のshape、色、軸の文字の大きさ、色、エラーバー、背景） - Qiita](http://qiita.com/yuifu/items/83103d03aef2dba95465)
* [Data visualization with ggplot2](http://www.rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf)(PDF)... RStudio謹製ggplot2のちーとしーと。ggplot2に慣れていないひとも慣れているひとも要ちぇっく

