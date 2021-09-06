# PFD

Process Flow Diagram

## これはなにか

PFD を GitHub Actions で描いてみようと思ったのでそれのお試し

## なぜ GitHub Actions なのか

* ドローイングツールで描くのは手軽で見た目もわかりやすいが、as Code で書いてみたかった
* ドローイングツールは見た目の部分に気を取られてしまいがちだと思ったため
* CI/CD のようなパイプライン定義はフローそのものに集中できると思ったから
* GitHub Actions の [Composite Action](https://docs.github.com/ja/actions/creating-actions/creating-a-composite-run-steps-action) がプロセス、input/output で成果物を表現できると思ったから
* GitHub Actions はワークフローのビジュアライズができるから [*](https://github.blog/changelog/2020-12-08-github-actions-workflow-visualization/)
* パイプラインを実行することで I/O のチェックや、フローの時間的エミュレーション、簡易的な評価などなんらかのアクションをできるから
* as Code されるということはレビューなどもしやすいと思ったから

## サンプル

### 業務プロセスの可視化に PFD を使ってみた話

[業務プロセスの可視化に PFD を使ってみた話](https://www.cresco.co.jp/blog/entry/16642/)

上記記事のサンプル PFD を模倣しました。

[![Process Flow Diagram](https://github.com/srz-zumix/PFD/actions/workflows/pfd-sample1.yml/badge.svg)](https://github.com/srz-zumix/PFD/actions/workflows/pfd-sample1.yml)

![image](https://user-images.githubusercontent.com/1439172/132120364-ef6f81e7-b9e5-4cb8-93a8-fb16e9268514.png)

## 書いてみた結果

### 工夫した点

* プロセス = Composite Action, 成果物 = Composite Action の Input/Output としたところ
  * Composite Action 内でブラックボックス的に擬似コードが書ける
  * Check $inputs ステップで空の成果物をチェックしたところ
* Composite Action の置き場所をスイムレーン的に階層わけしたところ 

### Pros/Cons

* Pros
  * Composite Action を用意すれば同じプロセスの使いまわしは簡単
  * as Code されるのは個人的に安心感あり
  * 見た目をキレイしようという考えがわかないので、フローに集中して書けた
  * I/O のチェックができるのは良い
    * このプロセスにはこのデータが必要だよねってのが書いててわかる
  * 未検証ではあるが 1min = 1day とかでエミュレーションとかもできるかも？
* Cons
  * I/O (成果物) のビジュアライズがないので PFD のイメージとしては課題が残る
    * I/O をリソースとして扱うような JFrog Pipelines とかだとリソースの流れも見やすいかも？（ビジュアライズされるかは未確認）
  * 書くのめんどくさい（これは PFD そのものにいえるが・・）
  * Composite Actions でプロセスと I/O 定義したらあとはビジュアルエディタで編集したい（GitHub Actions Beta のときのようなのが欲しい）

### 感想

アリかナシかで言ったら、ナシかな。
CI/CD のパイプラインで、リソース概念のあるものならもっといいのかもしれない。
それかオーバースペックな気がしないでもないが Unreal Engine のブループリント。

PFD をただ描くだけのドローイングツールはたくさんあるけど、
フローの正当性（ちゃんと成果物の I/O ができてるか）とか、改善のための ECRS を行ったりとか、
人間だけが図を見て、しかも手作業で描き直すのが面倒くさいと思ってるので、これを解決ツールがあると嬉しいなぁ。。
（見た目をキレイにしがちになるので、中身に時間をかけたいのよ）
