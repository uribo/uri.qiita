2014年版RStudioを使った文書作成法
=====

# はじめに

みなさま、**進捗どうですか**？　書類を作り、アウトプットするまでが文書作成です。というわけで、[文書作成 Advent Calendar](http://qiita.com/advent-calendar/2014/document)の14日目は、RStudio、Rmarkdownパッケージを使った文書作成の方法についてのまとめと自分が行っている文書作成の現状を書きます。

以下のものはパッケージに依存した機能なので、RStudioを使わずとも実行することができますが、**楽なので**という理由からRStudioを使った例を紹介します。

以前も同様の記事を書いていますので参考にどうぞ

* [RStudioを使ったPDF文書の作成（for RStudio 0.98.932+） - Qiita](http://qiita.com/uri/items/d9e50e8e5a37217a3f5d)
* [【まとめ】RMarkdown2で何が変わったのか？ - Qiita](http://qiita.com/uri/items/0c3b3f918f79b3e3e6d4)

## 実行環境

* OS: Mac OS X 10.10.1 (Yosemite)
* R version 3.1.2 (2014-10-31) -- "Pumpkin Helmet"
    * RStudio 0.98.1091
    * Rmarkdown
* Mac TeX 2014

# RStudioでのアウトプット

RStudioで文書を作成する際には以下の選択肢があります。

* HTML
* PDF
* Word
* Markdown

HTMLならファイル間のリンクができたり、各種HTMLタグが埋め込みできたりして便利ですが、やはり印刷物に向いているのはPDFな気がします。またTeXに関する知識があればパッケージによる機能拡張もできますので良い。

## プレゼンテーションも

次の形式でのプレゼンテーションファイルも作成可能です。	

* [Beamer](https://bitbucket.org/rivanvx/beamer/wiki/Home)
* [Google I/O](https://code.google.com/p/io-2012-slides/)
* [Slidy](http://www.w3.org/Talks/Tools/Slidy2/)


# PDF文書の作成

では実際にPDF文書を作成する方法です。

RStudioを起動し、File -> New File -> R Markdown...を選択し、アウトプットフォーマットの欄は`PDF`にします（後から変更することもできます）。

新規作成されたファイルを編集し、`Knit PDF`ボタンを押す（またはショートカットキー ⇧⌘K）でPDFが作成されます。

## YAMLの編集

文書の頭にある、ダッシュで挟まれた部分（YAML metadata）を編集することで文書の見た目や余白の調整が可能です。

```{r}
---
title: "Untitled"
author: "Author Name"
date: "YY-MM-DD"
output: pdf_document
---
```

## 日本語を含んだPDF文書

日本語を含む文書を扱う際には少し工夫が必要です。

Rmarkdownの文書作成は、Pandocによるレンダリングにより処理されており、LaTeXエンジンを`pdflatex`、`xelatex`、`lualatex`から選べます。

`ZXjatype`パッケージは`xelatex`に対応した日本語組版パッケージであり、それを使用することで日本語の文書を作成することができます。フォントの指定とともに、日本語文書向けに上記のYAMLメタデータを変更しましょう。

```{r}
---
title: "タイトル"
author: "俺"
date: "`2014年12月14日"
header-includes:
   - \usepackage{zxjatype}
   - \setjamainfont{Hiragino Kaku Gothic Pro}  
output:
  pdf_document:
    latex_engine: xelatex
---
```

YAMLの書き方は少し独特ですが、インデント（スペース２個）を使ってオプションを指定するというようなものです。

上の例では、`header-includes`オプションで`zxjatype`パッケージの読み込みとそのオプションとしてフォント（ヒラギノ角ゴプロ）の	指定を行いました。LaTeX的な書き方ですね。また、アウトプットオプションでPDFとして出力、その際のLaTeXエンジンにxelatexを使用する、という風な表現になっています。

ここまでで一応の日本語文書を作る準備ができました。

## 俺々な文書作成法

RMarkdownの文書中にLaTeXパッケージを使用することで、より美しく、さまざまな機能を含んだ文書を作れます。お気に入りのパッケージを使ってみましょう。今回は自分が使っている設定を晒します。

```{r}
---
title: "Change the title"
author: "Author Name"
date: "`r format(Sys.time(), '%B %d, %Y')`"
header-includes:
   - \usepackage{lscape} # 図を横に配置するためのパッケージ
   - \usepackage{zxjatype} # 日本語組版パッケージ
   - \setmainfont{Helvetica Neue} # 英語のメインフォント
   - \setjamainfont{Hiragino Kaku Gothic Pro} # 日本語のメインフォント
   - \setmonofont{Ricty} # Rスクリプト部分のフォント
   - \usepackage{soul} # 選択部分のハイライト表示に使うパッケージ
   - \newcommand{\HLT}[1]{\hl{{\bf \mbox{#1}}}} # 日本語部分のハイライトの定義
output:
  pdf_document:
    latex_engine: xelatex # zxjatypeパッケージを使用するために変更
    toc: true
    toc_depth: 3 # 見出しの表示とその深さを指定
    highlight: tango # Rスクリプトのハイライト形式
---
\fontsize{12}{18}
\hrulefill
```

## テンプレートの使用

いちいち上のYAMLを書くのも面倒なので、よく使う文書形式をテンプレートとして保存することができます（パッケージ化）。

あくまでも俺々用ですが、チャンクオプション（文書内でのRスクリプトの評価方法などを指定）と各種パッケージの読み込みを定義した`lab.note`パッケージを作成中なのでそちらも紹介します。

https://github.com/uribo/lab.note

こちらのパッケージを使用して作成した文書が以下のものです。

![名称未設定.png](https://qiita-image-store.s3.amazonaws.com/0/19462/8177d672-050e-61f3-87ee-1a3dfa90d55a.png)

データフレームの操作に便利な`dplyr`パッケージや作図に使用する`ggplot2`パッケージを標準で読み込むようにしています。他に便利なパッケージ（R, LaTeXどちらでも）があれば教えてください。

# おまけ

* [■knitrのデフォルトmarkdown.cssがくっそ見づらいから修正する - eizoo3010の日記](http://eizoo.hatenablog.com/entry/2014/07/06/012956)
* [R markdown(knitr)パッケージのchunk optionまとめ - My Life as a Mock Quant](http://d.hatena.ne.jp/teramonagi/20130615/1371303616)

# 参考

* [R Markdown — Dynamic Documents for R](http://rmarkdown.rstudio.com/)
* [The R Markdown Cheat Sheet | RStudio Blog](http://blog.rstudio.org/2014/08/01/the-r-markdown-cheat-sheet/)
* [rmarkdownパッケージで楽々ドキュメント生成](http://kohske.github.io/R/rmarkdown/)

