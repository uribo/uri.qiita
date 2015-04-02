# LaTeX文書中に絵文字的なものを取り入れる

絵文字（:rocket:や:ghost:など）をLaTeX文書の中に取り入れたいという願望があり、あれこれ方法を探したり試行錯誤してみたという苦労話。
結論は、**現段階**では**絵文字を使うことはかなり難しい**ということ。しかしその代わりに、絵文字ほどカラフルではないが、フォントアイコンなどを使ってLaTeX文書のおしゃれ感を増すことは比較的簡単にできる。

というわけで試行錯誤の記録と**Font-Awesomeを取り入れておしゃれ感を増す**方法を書きます。

## coloremojiパッケージによる絵文字の実装

`coloremoji`パッケージを使うことで、一応絵文字を使うことができます。ただし絵**文字**として扱っているのではなく、あくまでも**画像**として扱われている点に注意。

## LaTeX + Font-Awesome

`XeLaTeX`, `LuaLaTeX`に対応。フォントの種類も多く、おすすめです

Font-Awesomeについては下記ページをご覧ください

### 必要なもの

* `Font-Awesome`
    * 現時点（20150125）での最新版は4.3.0
    * http://fortawesome.github.io/Font-Awesome/ から必要なフォントをダウンロードし、インストール
* `fontawesome.sty`

### 基本的な構造

`\FaThumbsUp`のように`\Fa` + `icon名`を定義すれば対応するFont-Awesomeのフォントが出力される。

### 例

```tex
\documentclass[11pt]{report}
\usepackage{fontspec, fontawesome} % パッケージの読み込み

\begin{document}

\faFlag

\faRocket \faTwitter \faCopy

\end{document}
```

↓完成品
![test1502_pdf.png](https://qiita-image-store.s3.amazonaws.com/0/19462/0a9403b8-3e74-efd4-1363-48be9a05330e.png)

### fontawesome.styにないFontを表示させる

上記のfontawesome.styが対応しているFont-Awesomeはバージョンが古いので、新しいフォントがなかったりします。そういう場合には新しく定義することで出力が可能になります。プリアンブルに次のコマンドを記述します。

```tex
\providecommand\faGit{{\FA\symbol{"F1D3}}}
```

こうすることで`document`内で`\faGit`とすれば

が出力されます。適宜追加すると良いでしょう。

### Tips

LaTeXのコマンドと組み合わせて使うことで、いろいろできそうです

* 色をつける... `\textcolor{cyan}{\faTwitter}`
* 文字と組み合わせる（CSS的な処理）... `\Huge{\faCalendarEmpty}\textcolor{red}{{\Large{\hspace{-7mm}23}}}`
* 左右を反転... `\reflectbox{\faQuestion}`
* 傾ける... `\rotatebox{330}{\faQuestion}`