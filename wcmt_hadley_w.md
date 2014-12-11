羽鳥教入信のすゝめ
=====

## はじめに

![hadley.png](https://qiita-image-store.s3.amazonaws.com/0/19462/5637fa54-79ec-3663-bcb6-b46796c2f62f.png)

ここでいう羽鳥氏とは、Rの統合開発環境RStudioのチーフをつとめるHadley Wickhamさんのことです。誰が言い始めたのか不明ですが、日本での愛称です。

Hadley -> はどりー、はどれー -> **羽鳥**

今日はHadley Wickhamさんの紹介と、その信者（ただ単に羽鳥氏のふあん）について書きます。

## 神が神たる所以

神・羽鳥のすごさは、Rへの貢献の多さから伺えます。本、パッケージ、メーリングリスト、多くの場面で彼の名前を見つけます。**また羽鳥か...**、というくらいに。

Rの世界を知れば知るほど、彼の名前を見る機会が増えます。また、パッケージ制作に関わると彼から怒られることもあるとか。神の怒りに触れてはいけない（戒め）。

そんな羽鳥氏を尊敬し、崇拝する信者は、世界中にいるらしく、彼のRに対する思想やプログラミング、グラフィックスの作法を通称**Hadley World**というそうです。日本国内にも多くの信者がおり、**羽鳥教**として、使途としてRや羽鳥の素晴らしさを伝えるべく活動しています（対抗する神的存在はリゲスでしょうか...）。

### 羽鳥氏 on GitHub

https://github.com/hadley

羽鳥氏のGitHubページを見ると、この人たくさんコミットしてるなー、というのがコントリビューションを見るとわかるのですが、その量が尋常ではありません。さすが神。フォロワーもすごい...。

### 羽鳥作のパッケージ

一例

* [ggplot2](https://github.com/hadley/ggplot2)... 言わずと知れたグラフィックスライブラリ（なぜこれが標準パッケージでないのか謎）   
    * このRパッケージがすごい2014でも紹介
* [plyr](https://github.com/hadley/plyr)... 
* [stringr](https://github.com/hadley/stringr)... 文字列操作ライブラリ
    * このRパッケージがすごい2014でも紹介
* [scales](https://github.com/hadley/scales)
* [httr](https://github.com/hadley/httr)
* [devtools](https://github.com/hadley/devtools)... 開発者向けのライブラリですが、今となってはこちらも標準
* [dplyr](https://github.com/hadley/dplyr)... データフレーム変形、集計ライブラリ
    * このRパッケージがすごい2014でも紹介
* [reshape](https://github.com/hadley/reshape)
* [testthat](https://github.com/hadley/testthat)
* [lazyeval](https://github.com/hadley/lazyeval)
* [plotrix](http://cran.r-project.org/web/packages/plotrix/index.html)
* [lubridate](https://github.com/hadley/lubridate)

### <del>本</del>聖書

> 141210追記
また本を出版するみたいです。来年３月出版予定。かっちょいい表紙。

<blockquote class="twitter-tweet" lang="en"><p>Super excited about the cover for my new book! <a href="https://twitter.com/hashtag/rstats?src=hash">#rstats</a> <a href="http://t.co/1gXbZ6IHEZ">pic.twitter.com/1gXbZ6IHEZ</a></p>&mdash; Hadley Wickham (@hadleywickham) <a href="https://twitter.com/hadleywickham/status/542320716348014592">December 9, 2014</a></blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

神・羽鳥の著書はいわゆる聖書です。Rを使っている人ならば必需品というわけです（持っていないものがあるのでください）。

* **Advanced R**
    * この本の内容の大部分は[こちらのページの内容](http://adv-r.had.co.nz/)に準拠する
    * 2014年10月出版
    * 最新の知見とRの内部構造などについて書かれている。**聖書**。
* **R Package**
    * 本の内容はこちらをもとにするそうです -> http://r-pkgs.had.co.nz
    * Advanced Rの出版時に貢献し忘れた人はいますぐread & commit!!
        * PR出したら羽鳥から返事きた！（仕事早い） -> https://github.com/hadley/r-pkgs/pull/170
* **ggplot2: Elegant Graphics for Data Analysis**
    * ggplot2パッケージの詳細
    * 翻訳されています -> グラフィックスのためのRプログラミング - ggplot2入門
    * 毎夜、就寝前に読みたい...

## 神にまつわる情報

* 羽鳥氏のwebサイト -> http://had.co.nz/
    * [パッケージの作成方法](http://courses.had.co.nz/11-csiro/)についてや[データの可視化](http://courses.had.co.nz/11-ebay/)についての資料もあり、充実しています
    * [Wikipedia](http://en.wikipedia.org/wiki/Hadley_Wickham)にもページがあります（ページを作成、編集された信者の方、ご苦労様です）
* 神の教え（羽鳥氏はRStudio主催のセミナーで公演することがしばしばあります。ぜひチェックしましょう）
* かつて日本に降臨されたことがある
    * 2010年に統計数理研究所で開催されたセミナーに登壇
    * 素性が不明な羽鳥氏の一面についての貴重な記録 -> [Tutorial of ggplot2 by Hadley Wickham at ISM | Siguniang's Blog](https://siguniang.wordpress.com/2010/11/25/tutorial-of-ggplot2-by-hadley-wickham-at-ism/)
* 冒頭の肖像画は羽鳥氏です。さいごに、神を降臨させるスクリプトを紹介して終わります。ggmapパッケージ製作者はかなりの信者なのでしょう...。

```{r}
library(ggmap)
ggimage(hadley)
```


