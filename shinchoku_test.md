# 進捗を評価する関数を作った #進捗を支える技術

**進捗どうですか**。よい言葉ですね。私は、締め切り直前に追いつめられるよりも、くどくどと進捗状況を聞かれるほうが好きです。

さて、@dichika さんが自作の[yeahパッケージ](https://github.com/dichika/yeah)に素敵な関数を追加してくれました。目だけでなく、耳でも進捗を感じたいですよね（*今年は可視化の発展形として、可聴化なる言葉が流行るのでは...?*）。というわけで...

# shinchoku_test 進捗検定関数

**進捗検定ってなんだよ...**、という話ですが、目標のコミット数に応じて現在の進捗状況を判定してくれる関数が`shinchoku_test`です。

```r
shinchoku_test <- function (goal, num = 1) {
  commit <- system("git log --since='$(date +'%Y-%m-%d') 00:00:00' --no-merges --oneline | wc -l", 
              intern = T) %>%
    stringr::str_trim() %<>% as.numeric()
  
  yeah::doudesuka(num = num)
  Sys.sleep(2.0)
  print(paste("今日のコミット数は ", commit, 
              ifelse(commit < goal, 
               c(" 進捗だめです orz"), c(" 進捗あります!!"))))
}
```

実行するには、依存する`magrittr`、`stingr`および`yeah`パッケージをインストールしている必要があります。

では実行してみます。

```r
shinchoku_test(10)
#[1] "今日のコミット数は  6  進捗だめです orz"
```

残念ながら目標の進捗数に達していないみたいです😂

### 解説

`goal引数`は目標とするコミット数です。この値よりも一日分のリポジトリへのコミット数が多いか少ないかで結果が異なります。また、`doudesuka関数`内の`num引数`を変えることで、あなたの嗜好に応じた進捗検定（意味深）ができます。

## 参考

* [git "今日のコミット数"が知りたいときのワンライナー - Qiita](http://qiita.com/smd8122/items/2a8cee0516f98bb818f2)
    * `git shortlog`だと上手く行かなかったけど...
* [gitで指定期間のコミット回数や総追加行数などを取得するワンライナー - Qiita](http://qiita.com/takashibagura/items/6d03cdd9ab2f88df828d)

こちらからは以上です。よい進捗を👍