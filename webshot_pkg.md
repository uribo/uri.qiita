# Rを使ったスクリーンキャプチャ: webshotパッケージの応用

## はじめに

Rを使って、webページのスクリーンショットを撮影する[`webshot`](https://github.com/wch/webshot)パッケージというものがあります。

日本語での***使ってみた事例***が見つからなかった（[seekRで検索 150222](https://www.google.co.jp/cse?q=webshot&cx=partner-pub-6801897182966827%3A61726vqhhgw&ie=utf-8&hl=ja&sa=#gsc.tab=0&gsc.q=webshot&gsc.page=1)）のでQiitaでも紹介します。といいつつ、以前rpubsに記事を書いたのでそちらをご覧ください。

http://rpubs.com/uri-sy/demo_webshot

今回はその応用例を自分用にメモ書き。

## webshotパッケージの応用

スライド資料作成時に、Twitterのつぶやきを引用する（魚拓をとる）こととか、あると思います。そういうときにいちいちページにアクセスしてキャプチャを撮ると、都度サイズがばらついたり、無駄なスペースも含んでしまったりと、アレな感じです。

`webshot`関数では、スクリーンキャプチャを撮影する位置を引数によって指定することができますので、つぶやき部分のCSSセレクターを指定し、そんな面倒をなくすことが可能です。

実例↓ https://twitter.com/u_ribo/status/561669079430201344 のつぶやきをキャプチャします。

```r
library("webshot") # https://github.com/wch/webshot
webshot(url = "https://twitter.com/u_ribo/status/561669079430201344", 
        file = "webshot150222_1.png", 
        selector = ".expansion-container")
```

とすると、

![webshot150222_1.png](https://qiita-image-store.s3.amazonaws.com/0/19462/7e61ee57-4220-a3d1-9e6b-618c429d6c78.png)


このような画像ファイルが生成されます。ファイル拡張子は`png`形式以外にも、`jpeg`, `pdf`に対応しています。LaTeXならPDFにすると綺麗な図になりますね。

同様に、slideshareやSpearkerDeckのスライドを参照するときには次のように。

```r
webshot(url = "http://www.slideshare.net/uribo/data-pretreatment", 
        file = "webshot150222_2.png", 
        selector = "img.slide_image")
```

ちょっとしたtips。slideshareでは特定ページのアクセスはスライドのURLのサブディレクトリにページ番号、という形式になっているので、特定のページの画像が欲しいときはURLを`http://www.slideshare.net/uribo/data-pretreatment/22`のようにすると良いです。

```r
webshot(url = "https://speakerdeck.com/s_uryu/ecologist-must-use-git", 
        file = "webshot150222_3.png", 
        selector = "iframe.speakerdeck-iframe")
```

GitHubでの議論も魚拓をとってみます。ついでに`resize`関数でサイズ変更もしてみます。

```r github
webshot(url = "https://github.com/pilotmoon/PopClip-Extensions/pull/451", 
        file = "webshot150222_4.png") %>% 
  resize("120%")
```

![webshot150222_4.png](https://qiita-image-store.s3.amazonaws.com/0/19462/a85c8652-fbea-d24c-7ca3-99c55d46e93d.png)

ShinyAppのスクリーンキャプチャをとる`appshot`関数も用意されているのですが、自分の環境ではデモが正常に動きませんでした（なぜ？）。

他にもいろいろ使えそうですね。

## 注意点

自分以外のつぶやきやコメントなどをキャプチャする際は、用法用量を守って、正しくお使いください（著作権うんぬん）。

