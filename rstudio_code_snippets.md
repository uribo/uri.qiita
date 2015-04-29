# RStudio v0.99に搭載されたコードスニペット機能が便利

先日、RStudioのプレビューバージョンであるv0.99の機能の一つとして、コードスニペットが追加されたことがRStudio本陣から[告知されました](http://blog.rstudio.org/2015/04/13/rstudio-v0-99-preview-code-snippets/) 。私自身は、**コードスニペット？なにそれ美味しの？？**という反応でしたが、使ってみるとその便利さがくせになりました。

コードスニペットとは、ざっくばらんに言うと**頻繁に使用する定型的なコードを簡略なコマンド等で呼び出す**ことができる機能です。

コードを書いている最中、冗長な関数名を打つのが面倒になったり、関数内での引数がわからなくなることがRでもよくありますよね。例えばパッケージの読み込みや`apply()`など。１度ならまだしも、10のパッケージを呼び出すとなると、`library(hoge), library(piyo), ... library(foo)`と、長くなって嫌になりますし、時間の無駄です。

というわけで便利なコードスニペットを使いましょう。

コードスニペットを使うと、`library`と打つ手間が`lib (tabキー)`で済みます。`lib`とタイプし、tabキーを押せば、スニペットに登録された`library(package)`が呼び出され、`package`の部分を編集できる状態になります（呼び出しの`lib`も変更可能。`l`でも可能）。また、`apply()`の場合、`ap`とタイプした時点で`apply(snippet)`の補完が出てくるので、その時点でtabキーを押せば、`apply(array, margin, ...)`となって、`array`, `margin`の引数指定ができるようになります。sfihtキーで引数間を移動します。

これらはコードスニペットとして、それぞれ

```
snippet lib
	library(${1:package})
	
snippet apply
	apply(${1:array}, ${2:margin}, ${3:...})
```

が登録されているために実現可能となっています。`${}`内の番号と文字列が入力対象となります。文字列と番号はスニペット出力時の入力順や文字に対応しています。

## RStudioに実装されているコードスニペット

現在使用できるスニペットは、`R`, `C/C++`, `Markdown`, `JavaScript`, `HTML`, `CSS`, `SQL`, `Java`, `Python`の９種類です。編集中のファイル拡張子に応じて定義されたスニペットが利用可能になります。例えば拡張子`.R`や`.Rmd`のファイルであれば、スクリプト中あるいはチャンクコード内でR用のスニペットが使えます。

コードスニペットはMacの場合、（環境設定の画面 `cmd + ,`）メニューバーのRStudio -> Preferences... -> CodeにSnippetsという項目があるので、コードスニペットの利用を可能にするチェックをつけて利用可能になります。登録されているスニペットを確認するには、`Edit snippets...`のボタンを押してください。

## 俺々コードスニペット

RStudioのコードスニペットの素晴らしい点は、俺々スニペットの登録ができるところです。すでにいくつかのスニペットが登録されていますが、自分の好みに応じたスニペットを作成することができます。

自分は次のようなスニペットを登録しました。なおカスタマイズしたコードスニペットは`~/.R/snippets/`に保存されます。

```
snippet csv
	read.csv("${1:file}", header = TRUE)
```

なにはともあれ、csvファイルの読み込みを行うので、`csv`とタイプすることで読み込むファイルを指定できるようになります。他にもいろいろと俺々使用のコードスニペットを書いている最近です。はい。

```
snippet ggp
	${1:data} %>% ggplot(aes(${2:x}, ${3:y})) + geom_${4:type}()
	
snippet glm
	${1:data} %$% glm(formula = "${2:formula}", 
							 family = "${3:family}", 
							 data = .)
```	

ggplot2では、使用するデータと、グラフに表示させる変数（x, yそれぞれ）およびプロットのタイプをスニペットで入力できるようにしました。また、`glm()`のように引数が複数ある関数も、あらかじめ引数名を定義しておくことで入力間違いが減り、スムーズに実行できるようになりました。複雑で引数の多い関数ほど、コードスニペットの効果が発揮されるように感じます。

## お、そのコードスニペットいいじゃ〜ん、使わせてもらお

**あると思います**。そんなことを実現可能にするパッケージを[David Robinsonさん](https://github.com/dgrtwo)（[broom](https://github.com/dgrtwo/broom)パッケージの開発者）が作成してくださいました。

[dgrtwo/snippr](https://github.com/dgrtwo/snippr)

こちらの`snippr`を使うと、GistやGitHubリポジトリにあるみなさんの俺々スニペットを自分のコードスニペットに導入することができます（コピペとかナンセンス）。また`snippr`では、導入するスニペットの種類や特定のスニペットのみを選ぶこともできるので大変よろしいです。

使い方はこんな感じ。自分のものですが、[これ](https://github.com/uribo/snippets/blob/master/r.snippets)を導入するには

```r
snippr::snippets_install_github("uribo/snippets", language = "r")
```

とします。このようにするだけでGitHubリポジトリにある誰かのコードスニペットが使えるようになります。

自分の場合、ファイルの読み込みとプロット（plot, ggvis, ggplot2, ~~lattice~~）、各種検定や統計モデルの関数を登録しています。ほかにも便利なものがあれば随時...。

というわけで皆さんも（俺々コードスニペットを作成・公開して）enjoy!

## 最後に

LaTeXやチャンクコード自身を呼び出すsnippetが欲しいです。

<blockquote class="twitter-tweet" lang="en"><p>RStudio preview new feature `code snippets` are great! How I can define as knitr::chunk within .Rmd file?? <a href="https://twitter.com/hashtag/RStudio?src=hash">#RStudio</a></p>&mdash; ホクソエム (@u_ribo) <a href="https://twitter.com/u_ribo/status/591391118803083264">April 24, 2015</a></blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>