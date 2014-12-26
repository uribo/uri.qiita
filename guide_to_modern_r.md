一歩進んだRとの付き合い方
======

どうも、R歴４年目にしてR初心者勢です。こちらは**2015年にRをはじめたい、更に知識を高めたい人**に向けた記事と**自分の抱負**になります。

都度、参考になる本やURLを書いているので詳しくはそちらをご覧ください。

## これからRをはじめる、ほとんどR使っていない人向け

### はじめに: どうしてRなのか

よく言われることですが、

1. オープンソースでの開発 -> どういう機能をもっているか、どのように処理されるかがわかる
2. マルチプラットフォームでの利用 -> 環境を選ばずどこでも同じように作業できるというのは大事
3. 機能拡張（パッケージ、ライブラリ）に優れる -> 必要は発明の母の精神。俺がこういう機能欲しいから作るぜ★

ということを私は挙げます。

海外でもRは人気ですね -> [TIOBE Software: Tiobe Index](http://www.tiobe.com/index.php/content/paperinfo/tpci/index.html)（これからはじめたいプログラミング言語としてRとSwiftへの注目が高まっている）

比較的最近のR導入に関するスライドは[Hijiyama.R Entry session](http://www.slideshare.net/KojiKosugi/hijiyamar-entry-session)でしょうか。一読すると良いです。そういえば自分も導入記事を書いていました -> [Rプログラミングのための第一歩 - Qiita](http://qiita.com/uri/items/1245441ab179c6ee76f9) （まだ未完） 

### 環境の整備

環境は大事です。個人の好みですが、最低限の環境は揃えるのが良いかと思います。とりあえず、Rをインストールしたあとは

* RStudioのダウンロード、インストール
* GitHubのアカウントを作成
* `motivator`パッケージのインストール

をしましょう。

#### RStudioについて

[RSutdio](http://www.rstudio.com)はRの統合開発環境(Integrated Development Environment: **IDE**)です。
2011年にリリースが[はじまりました](http://blog.rstudio.org/2011/02/28/rstudio-new-open-source-ide-for-r/)

![](https://github.com/YokohamaR/yokohama.r/wiki/src/images/startup-rstudio.png)

上の画像のように、４つのパネルに分割されているのが特徴で、画面一つでコードを書いたり、アウトプットの確認ができます。ヘルプの参照も楽です。変数、関数名の候補出力、パッケージのインストールや更新も便利な機能のひとつです。

RをインストールしていてRStudioを使っていない人をみると、崇拝するエディタがあるなど、宗教上の理由がある場合をのぞいて、**なんで使ってないの（憤怒）となります**。

> ##### 超絶便利なショートカットキー
もっと早く知りたかった、というもの。まずは**Option + Shift + K**（Macの場合）を押してください。しゅごーいいいいいいいい。現場からは以上です

RStudioを扱っている本は少ないですが、私の知っているものでは以下のものがあります。

* Mark P. J., Van Der Loo, Edwin De Jonge (2012). Learning RStudio for R Statistical Computing. *Packt Publishing*
    * Kindleで1000円ちょいと割安。良い。
* John Verzani (2011). Getting Started With RStudio. *Oreilly*
    * 読んでいない
* 石田基広 (2012). Rで学ぶデータ・プログラミング入門 RStudioを活用する. *共立出版*
    * 日本語での良書。Gitについても書かれている

#### GitHub

プロジェクトやコード、自作関数の管理は[GitHub](https://github.com)で行いましょう。公開したコードについて、誰かがコメントをくれたり、改善策を出してくれるかもしれません。

最近ではパッケージの開発をGitHubで行う人が増えています。`devtools`パッケージを使えば、GitHubの開発版パッケージ（CRANに登録しない、されない人もいるので）をインストール可能です。

おすすめ本

* 岩松 信洋, 上川 純一, まえだこうへい, 小川 伸一郎 (2011).Gitによるバージョン管理. *オーム社*
    * 最近買った良書。細かく書かれているし、わかりやすい
* 大塚弘記  (2014). GitHub実践入門. *技術評論社*

#### motivator: 進捗どうですか？

進捗状況を可視化できるとモチベーションの維持・向上につながります。というわけで、手前味噌ですが[`motivator`](https://github.com/uribo/motivator)パッケージを作りました。たくさんコードを書きましょう！

![](https://github.com/uribo/motivator/raw/master/inst/assets/img/demo_activity_log.png)

### hadleyverse

Hadley本人に楽しんでいただけた

<blockquote class="twitter-tweet" lang="en"><p><a href="https://twitter.com/kohske">@kohske</a> the google translation is pretty hilarious: <a href="https://t.co/SOH8KZg87P">https://t.co/SOH8KZg87P</a></p>&mdash; Hadley Wickham (@hadleywickham) <a href="https://twitter.com/hadleywickham/status/543836371270389763">December 13, 2014</a></blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

ので、調子に乗ってここでも布教活動をします（だって使徒だし...）

羽鳥教については以前の記事をご覧ください

ref) [R - 羽鳥教入信のすゝめ - Qiita](http://qiita.com/uri/items/a66b682507181baa0d50)

特にグラフィックスは標準のものよりも`ggplot2`パッケージを使うと良い。きれいだし、自由度が高いので慣れると便利です。

また、上述の`devtools`も欠かせないですね...。

ちなみに

<blockquote class="twitter-tweet" lang="en"><p>Hadley Wickhamのパッケージ群で回る世界をさす言葉としてはhadleyverseっていうのもよく見ますね。彼が作った有用なパッケージ群を中心にRの環境を整えてくれる同名のdocker-imageもあります <a href="https://t.co/kVocuZyJ5J">https://t.co/kVocuZyJ5J</a></p>&mdash; イルミ最高 (@dichika) <a href="https://twitter.com/dichika/status/542276639917236224">December 9, 2014</a></blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

## Rともっと仲良くなりたい人向け（2015年私の抱負）

R周りの変化は結構激しいです。どんどん新しいものが出てきます。*あなたの知識は最新ですか？*

### Pipe: こういう書き方もあります

処理を続けていく際、

```{r}
library(dplyr)
df <- data(iris)
df <- filter(iris, Species == "setosa")
df <- summarise(df, MIN=min(Sepal.Length),
                 MEAN=mean(Sepal.Length),
                 MEDIAN=median(Sepal.Length),
                 MAX=max(Sepal.Length))
```

としたり、

```{r}
max(subset(data.frame(x = 1, y = 1:10), y > 5))
```

というようなネスト構造のコードは、Pipe演算子 `%>%`を使えばわかりやすく表現することができます。はじめの例では

```{r}
library(dplyr)
library(magrittr) # dplyrと同時に読み込まれるけど...
df <- iris %>%
  filter(Species == "setosa") %>%
  summarise_each(funs(min, mean, median, max), Sepal.Length)
 ```

詳しくは... [このRパッケージがすごい2014 - Qiita](http://qiita.com/uri/items/ce711ee6da76a1e11ca5)での[magrittr](http://rpubs.com/uri-sy/demo_magrittr)紹介記事をどうぞ。

> #### 今、hoxo_mさんから目が離せない
あま●んのようなアイコンの人がいます。id: hoxo_mさんです。最近、hoxo_mさんが作成されたパッケージが熱いと私の中で話題です。
* **[lambdaR](http://d.hatena.ne.jp/hoxo_m/20141204/p1)** -> R にラムダ式を導入
* **[pforeach](http://d.hatena.ne.jp/hoxo_m/20141222/p1)** -> R で超簡単に並列処理

### 自作関数を作ろう、パッケージにして世界に公開しよう

まだまだ関数についての知識が足りないですが、関数を作るのは楽しいです。世の中には数えきれないほどのパッケージがあります。くだらないパッケージもたくさんです。でもそのパッケージを誰かが使えば、ひょっとしたら役に立つかもしれません。その人の関数作成の時間を省略することにもなります。関数をじゃんじゃん書いて、公開してみましょう。

またRStudioを使えばパッケージの作成が楽にできます。

> #### 便利なショートカット: 関数の抽出（定義）
たとえば、通常のコードを書いていて、**これ関数にしよ**と思うわけですが、関数となるコードを選択して**Option + Command + X** (Macの場合)で関数名を定義するポップアップが出てきて、適当な名前をつけるとあら不思議、コード内で使用した変数を自動的に引数とした関数を作ってくれます

本とSlideShareへのリンク

* 金明哲 編 (2014). Rのパッケージおよびツールの作成と応用. *共立出版*
    * 新しい本（2014年12月刊行）。Rcppごりごり使うぜ！という人には良い
* [Rパッケージ作成ハドリー風: devtools, roxygen2, testthatを添えて](http://www.slideshare.net/kaz_yos/r-devtools-roxygen2?related=1)
    * Tokyo.Rで直接聞いた話。私はこれでパッケージ作成をはじめました
* [東京R非公式おじさんが教える本当に気持ちいいパッケージ作成法](http://www.slideshare.net/teramonagi/r-38511360)
    * Hadely ありがとう。ネ申!! teramonagi さんありがとう。大イム!!
* [Data scienceをきわめて個人的な意思決定に活かす - 東京で尻を洗う](http://d.hatena.ne.jp/dichika/20141214/p1)
    * すごく、よく、わかる。納得の一言

### セミナー・勉強会に参加しましょう

勉強する気がなくても、マニアックな話が聞けるので得るものが多いです。適宜、近い場所のセミナーにでもいけばいいんじゃないかな。

| Name | Organizer | Place |
|------|-----------|-------|
| HiRoshima.R (HijiyamaR) | [@sakaue](https://twitter.com/sakaue) | Hiroshima, Hiroshima |
| [Kashiwa.R](http://www14.atwiki.jp/kashiwar/) | [@Acafe_info](http://twitter.com/Acafe_info) | Kashiwa, Chiba |
| [Kobe.R](http://kobexr.doorkeeper.jp) | [@h_kawahara](https://twitter.com/h_kawahara), [@florets1](https://twitter.com/florets1)  | Kobe, Kobe |
| [Nagoya.R](http://corpus-study.info/nagoyar/) | [@kwsk3939](https://twitter.com/kwsk3939) | Nagoya, Aichi |
| [Okinawa.R](http://www.okada.jp.org/RWiki/?%B2%AD%C6%ECR%C6%B1%B9%A5%B2%F1) (沖縄R同好会) | - | Naha, Okinawa |
| [Osaka.R](https://sites.google.com/site/osakarwiki/) | [@phosphor_m](http://twitter.com/phosphor_m) | Osaka, Osaka |
| [SappoRo.R](http://kokucheese.com/event/index/88324/) |  [@uranoken](https://twitter.com/uranoken) | Sapporo, Hokkaido |
| [Shiga.R](http://atnd.org/events/5939) | - | - |
| [Tokyo.R](https://groups.google.com/forum/#!forum/r-study-tokyo) | [@yokkuns](http://twitter.com/yokkuns) | Tokyo, Tokyo |
| [Tsukuba.R](http://seesaawiki.jp/w/syou6162/) | - | - |
| [Yokohama.R](https://github.com/YokohamaR/yokohama.r) | [@uribo](http://twitter.com/u_ribo) | Yokohama, Kanagawa |

ガチ勢は**UseR!@Aalborg, Denmark**（R利用者の国際カンファレンス）へどうぞ。おそらく12月に開催されるであろう**Japan.R**でも良いですね。

<blockquote class="twitter-tweet" lang="en"><p>We are excited to announce the first confirmed speaker at useR! 2015 <a href="https://twitter.com/hashtag/useR2015?src=hash">#useR2015</a> in Aalborg, Denmark: Thomas Lumley <a href="https://twitter.com/tslumley">@tslumley</a> (R Core, Survey)</p>&mdash; useR! 2015 Aalborg (@user2015aalborg) <a href="https://twitter.com/user2015aalborg/status/486098326014951424">July 7, 2014</a></blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

### 情報を公開する

ブログ、[rpubs](https://rpubs.com)、[gist](https://gist.github.com)、[Qiita](http://qiita.com)、Twitterなんでも良いです。

ありがたいお言葉があります。

<blockquote class="twitter-tweet" lang="en"><p>エンジニアだけでなくデータ解析者もブログはやるべき！いいポジションがあってもブログかgithubがないと推薦もできん。</p>&mdash; berobero (@berobero11) <a href="https://twitter.com/berobero11/status/540084640711593985">December 3, 2014</a></blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

私はもっとRの記事が読みたいです。**なので皆さんどんどん書いてください**。私自身はこうしてQiitaにちまちま投稿するくらいなので来年はがんばりたいところ

> #### よく読んでいるブログ（国内）
皆さま、各自の特色がでていて、最新の知識や技術も積極的に導入しているので勉強になります。
* [東京で尻を洗う](http://d.hatena.ne.jp/dichika/)
    * yeah::zoi()、きもちいいいいいい！R記事、お世話になっています
* [My Life as a Mock Quant](http://d.hatena.ne.jp/teramonagi/)
    * ご存知大仏さま
* [gepulog](http://blog.gepuro.net/)
    * 今年のJapan.Rの主催者のひとり。ねっとあいどるのげぷろくんです
* [ほくそ笑む](http://d.hatena.ne.jp/hoxo_m/)
    * 統計解析なんかの勉強にも良いです
* [捨てられたブログ](http://blog.recyclebin.jp/)
    * 力がほしいか（Rに詳しくなりたいなら必読）
* [300億円欲しい](http://gg-hogehoge.hatenablog.com/)
    * 面白い。最近、やきゅーデータの解析がないですね...
* [驚異のアニヲタ社会復帰への道](http://d.hatena.ne.jp/MikuHatsune/)
    * 小難しい内容を楽しい感じで紹介してくれます
> 他にはR-bloggeres（世界のRに関する記事を紹介してる）の購読は欠かせないところ

### 再現性を高めよ

同じことを繰り返し書くのはめんどくさ子さん。多量のファイルやファイルの管理に悩みたくない...。そんな人は`rmarkdown`パッケージとGitHubを使ったバージョン管理をしましょう。比較的簡単に（日本語関連の闇は深い）reproducibleな文書作成ができます

参考に -> [2014年版RStudioを使った文書作成法 - Qiita](http://qiita.com/uri/items/5cce4431ad0d96b96689)

### 可視化、しよう

**インタラクティブ**にね。というわけで以下の知識を深めると良い

* [Shiny](http://shiny.rstudio.com)
* Javascript ([htmlwidgets](http://www.htmlwidgets.org))

### ...高みへ

並列処理とか高速化とかよくわからんですが、ご利益がありそうなので勉強したい

* 正規表現
* Rcpp

# おわりに

最近、神・羽鳥が書いた文書（[Hadley Wickham: Impact the world by being useful « IMS Bulletin](http://bulletin.imstat.org/2014/12/hadley-wickham-impact-the-world-by-being-useful/)）を読んで、ついかっとなって書きました。書きなぐりのような文章で、全体でまとまりがなくなってしまいました。振り返ってみると、私自身の2014年版Rに関する知識の総決算、という感じですね...。これからもRと仲良くやっていきたいです。みなさんもR, RStudio, GitHubもっと使っていきましょう。