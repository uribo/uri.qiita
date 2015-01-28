# インストールしたRパッケージのあれこれ

**について調べている。**同様のことは以前、@R_Linuxさんが書かれている（[R - パッケージの出所を確認 - Qiita](http://qiita.com/R_Linux/items/4c3ccdbe61c088fac008)）のだが、そこで触れられていないことをメモ代わりに。

## パッケージのインストール先

パッケージのインストール先（ディレクトリ）を知りたいときには`find.package`, `path.package`の２つの関数を使うと良い。

```r
find.package("dplyr")
path.package("ggplot2")
```

この２つの関数の違いは、すでにパッケージが読み込まれているかどうかで挙動が変わってくる。目的のパッケージを読み込んだ後であれば`path.package`で良いが、読み込む前ならば`find.package`を使用しないとパッケージは見つからない。

## パッケージのバージョンを知る

パッケージの情報を得るには、@R_Linuxさんの記事にある`packageDescription`関数を使えば良いのだが、そんなにいろいろな情報は知りたくない。**パッケージが新しいかどうかだけを知りたいんじゃ**というときには`packageVersion`関数が有効。

## パッケージのvignetteを呼び出す

Rパッケージには、パッケージおよび関数の説明が書かれたファイルとは別に、パッケージの使用方法や解説などが書かれたvignetteを備えている場合がある（個人的にvignetteを用意している開発者は親切な方なのだろうなと思う）。そんなときには`vignette`関数にパッケージ名を引数で渡すことで呼び出すことができる（ちょいと時間がかかる）。vignetteを用意していないパッケージであれば、vignetteがない旨を知らせるエラーを返す。

### インストールしているパッケージのvignetteを一覧する

`browseVignettes()`でブラウザが起動する。

## パッケージの内部ファイルのパスを得る

自身のパッケージで使用しているファイルなど、使うときは限られるだろうが（ディレクトリ構造を理解していないと...）。

```r
system.file("csv/uspop2000.csv", package = "leaflet")
```

個々の環境により、パスは変わってくるので、一度こちらで得たパスを代入しておくと、[yeah::detayo](https://github.com/dichika/yeah/blob/master/R/yeah.R#L19)のようなことも可能になる。

## おまけ

関係ないが、良いページを見つけた。良い開発者になるためにvignetteの書き方も覚えたいところ。

[Vignette | Rパッケージ用vignetteの書き方](http://stat.biopapyrus.net/dev/vignette.html)

もう一つおまけ。見覚えのある盾アイコンのクールなhrbrmstrさん（ほかにもナイスなパッケージがある）が開発されている[dtupdate](https://github.com/hrbrmstr/dtupdate)を使うとGitHubからインストールしたパッケージの更新情報を知ることができる。

## 参考

* Rプログラミングマニュアル 第２版 -Rバージョン３対応-. 間瀬茂 2014. **数理工学社**