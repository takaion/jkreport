# jkreport.sty
じょっこーのためのLaTeXスタイルファイル
version 1.0.2

## 概要
じょっこー用レポート表紙をLaTeXスタイルファイルとして実装しました．
Word，LaTeXそれぞれで表紙と本文のPDFを作成して連結させる必要がなくなります．

追記: Cloud LaTeX にて動作を確認しました．（2017年1月19日確認）

## レポート作成を，より快適に
レポートを書いていたとき，こんな場面に遭遇したことはありませんか？

- 図や表，数式が多すぎて番号をふるのが大変… レイアウトの調整もつらい…
- 文書を保存しようと思ったら原因不明のフリーズに見舞われ，進捗が全て白紙に…
- すでにLaTeX でレポートを書いてはいるけど，表紙と本文を結合する手間が面倒…

jkreport.sty を使えば，これらの問題は全て解決です．

## インストール
texmf-local/texディレクトリに入れるか，あなたのレポート用.texファイルがあるディレクトリに入れてください．
texmf-localディレクトリについては，TeX Wikiの[この記事](https://texwiki.texjp.org/?TeX%20%E3%81%AE%E3%83%87%E3%82%A3%E3%83%AC%E3%82%AF%E3%83%88%E3%83%AA%E6%A7%8B%E6%88%90)に詳しく記載されています．
texmf-localディレクトリに入れることで，何回もjkreport.styをコピーする必要はなくなりますが，mktexlsrコマンドを実行しなければLaTeXのコマンドに認識されないことに注意して下さい．

### 依存ライブラリ
jkreport.styを使用するためには，以下のライブラリが必要です．
jkreport.styとともにtexmf-local/texディレクトリに入れるか，あなたの.texファイルがあるディレクトリに全て入れて下さい(あまりおすすめしません)．

- tlarray ([ダウンロード](https://github.com/wtsnjp/TLArray))
- tikz ([TeX Wikiによる説明](https://texwiki.texjp.org/?TikZ)，[ダウンロード](http://www.ctan.org/pkg/pgf))
- geometry ([TeX Wikiによる説明](https://texwiki.texjp.org/?geometry)，[ダウンロード](https://www.ctan.org/pkg/geometry))

tikz，geometryパッケージは，`tlmgr`を使えば簡単にインストールできます: `tlmgr install pgf geometry`

## 使い方
### 読み込ませる
`\documentclass{jsarticle}`などと`\begin{document}`の間(プリアンブル)に`\usepackage{jkreport}`を挿入して下さい．また，TikZはgraphicxパッケージによる初期設定が必要なため，書いておく必要があります．PDF化することが大半だと思うので，`\usepackage[dvipdfmx]{graphicx}`を挿入しておけばOKです．

以下のようになればOKです．

```
\documentclass{jsarticle}
\usepackage{color}
\usepackage[dvipdfmx]{graphicx}
\usepackage{jkreport}

\begin{document}
〜本文〜
\end{document}
```

注意: `sample.tex`，`template.tex`では`\documentclass[uplatex]{jsarticle}`となっています．これは，upLaTeX をエンジンとして使用するためです．他のエンジン（pLaTeX，XeLaTeX など）を使用する場合は，適宜変更してください．

### 変数を設定する
デフォルトで使われているtitle，author，dateの少なすぎる項目の代わりに，jkreport.styは以下の項目をマクロで変数的に使えるようにしました．

- `\classname{科目名}`で科目名を設定します．
- `\credits{単位数}`で科目の単位数を設定します．
- `\semester{学期}`で学期を設定します．
- `\teacher{担当教員名}`で担当教員名を設定します．
- `\title{テーマ番号・テーマ名}`でテーマ番号・テーマ名を設定します．
- `\grade{学年}`で学年を設定します．
- `\studentid{学籍番号}`で学籍番号を設定します．
- `\author{氏名}`で氏名を設定します．
- `\partner{共同実験者}`で共同実験者を設定します．6人まで登録可能で，書いた順に上から表示されます．
- `\dateOfExpm{実験日}`で実験日を設定します．6日分まで登録可能で，書いた順に上から表示されます．
- `\submit{提出日}`で提出日を設定します．5日分まで登録可能で，書いた順に上から表示されます．
- `\deadline{提出期限}`で提出期限を設定します．5日分まで登録可能で，書いた順に上から表示されます．

### 表紙を生成する
変数を設定したら，`\maketitle`で表紙ページを生成します．
その後はいつも通りに本文を書いていくだけです．

### フォントサイズを変えたい場合
LaTeX 標準のフォントサイズは10ptとなっています．このサイズが小さいと感じたときは，たとえば次のコマンドを`\maketitle`の直後に置いてください．

- `\fontsize{11pt}{17.6pt}\selectfont`

この場合，文字のサイズが11pt，行送りサイズが17.6ptとなります．

注意: `\documentclass[11pt]{jsarticle}`と設定すると，表紙の体裁が大きく崩れてしまいます．フォントサイズを変更したい場合は，上記の方法でお願い致します．

### Cloud LaTeX の場合
Cloud LaTeX の場合，TikZ，geometryはあらかじめ使用できるように設定されています．したがって，新たに追加すべきスタイルファイルは，tlarray.sty，jkreport.sty の2点となります．その他の点は，上記と変わりません．
