# Rで絵文字（sushi <- c(:sushi:)への道）

## はじめに

私事ですが、著名なシリアルパッケージクリエイターである@dichikaさんがピザを食べながら言っていた言葉が頭に残っています。

> sushiに:sushi:を代入したい

その熱意と言葉に**夢を感じました**。

それからちょくちょく、どうすればRで:sushi:を食えるか、否、絵文字を使えるかということを考えていて、Twitter上でぶつぶつとつぶやいたり、Qiitaに記事を書いたり、絵文字使いたい勢とやり取りをしていたのですが、海の向こうにもR上で~~寿司を食べたい~~絵文字を使いたい人がいるみたいで、素晴らしいパッケージを作成してくれました。ありがとう:cat: 感謝です。

そんなわけでRで絵文字を扱える`remoji`:package:パッケージを日本のRで絵文字使いたい勢に届けます。ほとんどREADMEの内容ですがあしからず。

## remojiパッケージ

まだCRANには登録されていないみたいなので、`devtools`パッケージを使ってGitHubからインストールします。

```r
devtools::install_github("richfitz/remoji")
library("remoji")
```

### 絵文字を使う

```r
message(emoji("cat"))
```

猫の絵文字:cat:が表示されました。では本題の寿司を召喚したいと思います。どういう理由かわかりませんが、`message`関数をかませる必要があるみたいですね。

```r
message(emoji("sushi"))
```

ｷﾀ━━━━(ﾟ∀ﾟ)━━━━!!嬉しいので回転寿司（多重寿司分身の術）にしてみます。お茶も欲しいですよね。ということで。

```r
message(emoji(c("sushi", "tea"), pad = TRUE)[c(1, 1, 1, 1, 1, 1, 2)])
```

:sushi: :sushi: :sushi: :sushi: :sushi: :sushi: :tea:

#### 寿司食べたい :sushi:

文字列と絵文字を組み合わせる場合には、先程同様、`message`関数と**`sub_emoji`関数**を使用します。

```r
message(sub_emoji("寿司食べたい :sushi:"))
```

### 使用可能な絵文字

絵文字を表示させるには、絵文字を表わす文字列を知っている必要がある（sushi -> :sushi:はできるが:sushi: -> 寿司はできない）ので、`list_emoji`関数という一覧を取得する関数で使用可能な絵文字を把握できます。

では逆に、本物の絵文字一覧を表示するには？というと、READMEにあるように

```r
message(emoji(list_emoji(), TRUE))
```

をすればコンソールがカラフルな絵文字で埋め尽くされます。

#### 絵文字を探す

この絵文字ってこういう文字列だったかなー、というときに便利な関数も用意されています。

```r
find_emoji("sun") %>% emoji_table()
```

関連する絵文字とその文字列が表示されました。やったぜ。

ちなみに、存在しない絵文字を与えると怒られます笑

```r
find_emoji("yakiniku") %>% emoji_table()
```

## おわりに

寿司が一歩近づきました。素晴らしいです。とはいえ、先述したように「:sushi: -> 寿司」ができないというような課題もあります。`plot(~, pch = `:beer:`)`みたいなことも無理なわけで...。

絵文字スキーな皆さん、どうぞお力添えを。

## 参考

* [richfitz/remoji](https://github.com/richfitz/remoji)
* [:sushi: - Technically, technophobic.](http://notchained.hatenablog.com/entry/2015/02/02/233112)
* [R - ソースコードの中でも絵文字を使う :rocket: #進捗を支える技術 - Qiita](http://qiita.com/uri/items/e27adda87bb0c32f18ff)


