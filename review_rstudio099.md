# RStudio 0.99の変更点と最近のRコードの書き方

先日、めでたくRStudioのversion0.99が[プレリリース](http://www.rstudio.com/products/rstudio/download/preview-release-notes/)となりました

<blockquote class="twitter-tweet" lang="en"><p>RStudio v0.99 Preview Release (enhanced code completion, new data viewer, and more): <a href="http://t.co/Zc0Jeqc9mD">http://t.co/Zc0Jeqc9mD</a> <a href="https://twitter.com/hashtag/rstats?src=hash">#rstats</a></p>&mdash; RStudio (@rstudio) <a href="https://twitter.com/rstudio/status/559759861987426304">January 26, 2015</a></blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

RStudio大好きおじさんなので、**RStudio 0.99の変更点**についてのまとめと使用レビューをしてみます。実行環境がMacなため、Mac以外OSをご使用の方は適宜コマンドやメニューをご自身の環境に合わせてお試しください。

公式Twitterでも言っている特に0.98からの大きな変更点は２点

* コードの補完性の向上（**パッケージ名**、変数名、関数名）
* 新しいデータビューア（`DT`パッケージの埋め込み？）

大きな変更点からみていきます。

詳細な変更点については[公式ページ](http://www.rstudio.com/products/rstudio/download/preview-release-notes/)を参照してください。

## コードの補完性の向上

これまでRStudioでは関数名やデータフレームの変数の（`tab`キーによる）補完をしてくれていましたが、パッケージ名の補完はできませんでした。0.99では、コンピュータにインストールしてあるパッケージ名を補完する機能がついています。

パッケージの読み込み時の挙動は`library`でも`require`でも同じです。

![lJY8b4UkCQ.gif](https://qiita-image-store.s3.amazonaws.com/0/19462/bbac89fd-9c14-7c40-0221-7f60fcf978d5.gif)

候補となる表示がでると、パッケージ、関数に応じた概要を出してくれるのも良いですね。この時点で、詳細なヘルプを見たい場合は、以前と同じく`F1`キーを押すとヘルプパネルにヘルプが表示されます。

![RStudio.png](https://qiita-image-store.s3.amazonaws.com/0/19462/57f01b98-d47d-f1f2-7ee2-a91f25fced64.png)

Rだけでなく、C, C++についても補完してくれるようです（LaTeXにも対応しないかな）

### ファイルの補完

`read.csv("")`とした時に、`tab`キーを押すことで、候補となるファイル名を表示してくれます。階層の深いフォルダにあるファイルでも探せるので、ファイル名さえ覚えていればディレクトリを記述する手間が省けて便利です。

## 新しいデータビューア

あるつぶやきをもとにしたこんな話がありました。

[データフレームの中身を確かめる - 東京で尻を洗う](http://d.hatena.ne.jp/dichika/20141121/p1)

いつもどおり、データフレームを表示する`r View(iris)`を実行してみてください。Viewパネルの変化にお気づきでしょうか。

新しいViewパネルでは、データフレームの値の検索やソーティング、フィルタリング、パネルの独立が可能になりました。やったぜ。

これで文句ないですね。


### プロットパネルの解像度の変更

retina, 高解像度のディスプレイに対応して、より綺麗なプロットが表示されるようになりました。

## コンソール、ソースパネルのスタイルの統一と新スタイルの追加

これまでは、ソースパネルのみに適用されていたスタイル（メニューバー RStudio -> Preference -> Appearance -> Editor themeで設定）が、コンソールにも適用されるようになりました。また、テーマ自身もかなり増えて、選択の幅が広がっています。お好みのテーマでEnjoy!

ちなみに私はコメントが斜体になる（日本語も）ので`Dawn`テーマを使っています。

### ソースパネルタブの並び替えが可能に

複数のファイルを開くと、ソースパネルがぱんぱんになるわけで、これを並び替えることができるようになりました。

## ショートカットキーでパイプラインを挿入した時の挙動

細かいところですが、パイプライン %>% をショートカットキー（`⌘⇧M`）で挿入した時の挙動はその場で以改行する仕様でしたが、少し変わったみたいで、改行をしなくなっています。


```r
iris %>% 
  filter(Sepal.Width >= 4)
```

これが

```r
iris %>% filter(Sepal.Width >= 4)
```

こう。ちょっとしたパイプなら改行しないほうが見やすいコードですね。


-----

## 最近のRコードの書き方

おまけです。

### パッケージ名を引用符で囲う

RStudio 0.99で実装されたように、Rでのパッケージ名の読み込みにはパッケージ名をクオーテーションで囲うようにしました。また、`glm`などで`family`引数に渡す値にもクオーテーションを使うようにしました（i.e.) `family = "binomial"`）。

どちらの場合もクオーテーションがなくても動作するわけですが、オブジェクト名と厳密に区別しようという気持ちからです。

~~もうひとつ。パイプラインでつないだ関数に渡す引数がない場合、`xtable()`とかになりますが、ここでの括弧は省略してもいいかなと思うようになりました。~~

↑`tab`キー補完をしたときはカギ括弧がついているので、そちらの挙動と合わせるためにやめた。

**150208追記**

情報量が少なかったので追記しました。

### ソースコード内に絵文字を使う

先日、ソースコード等における絵文字の有効性について[書きました](http://qiita.com/uri/items/e27adda87bb0c32f18ff)。反響がなくて悲しいところです。なのでここでも普及活動。RStudioでは、チャンクや関数間へジャンプできる機能がありますが、これも絵文字を使っていると認知性が上がると思います。

before ↓
![without_emoji.png](https://qiita-image-store.s3.amazonaws.com/0/19462/53226b83-edc2-1688-678b-bf78ee233f29.png)

after ↓
![with_emoji.png](https://qiita-image-store.s3.amazonaws.com/0/19462/bad5cbe5-8303-d47d-e97f-67c1484e01db.png)

### 自作関数名には「.」（ドット）を使わず「_」（アンダースコア）を使う

Hadleyが言っていた気がします（出所・URL不明。判明次第リンクはります）。Hadley作の関数では、これが統一されています（`geom_bar`, `filter_`など）。統一する、というのが大事なところでしょうか。

### 対になるもの、いくつかの組み合わせは一行ですませる

これまで、x軸y軸にラベルをつける際に

```r
ggplot(~) +
  ... +
  scale_x_continuous("hoge") +
  scale_y_continuous("piyo")
```

というように`scale_x_continuous`と`scale_y_continuous`をいちいち改行していましたが、改行をやめた、というだけ。

また、ある条件ごとに`subset`なり`filter`したデータフレームへの代入も、**セミコロン ;**を使って連結するようにしています。

**皆さんの最近の知見など、どこかに書いてくれると嬉しいですね**
