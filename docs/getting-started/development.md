---
layout: docs-getting-started
toc: toc-user-guide.html
title: ソースからNode-REDを実行する
slug: ソース
---

ソースからコードをビルドし、実行することは、
開発コードを利用することが好きなユーザまたはプロジェクトに貢献したい開発ユーザのみ、
目指すことです。

### 必須条件

ソースからNode-REDを実行するためには以下のことが必要です:

 - [サポートされているNode.jsのバージョン](/docs/faq/node-versions)
 - `git`クライアント
 - グローバルインストールされたnpmモジュール`grunt-cli`
```
sudo npm install -g grunt-cli
```

### コードのクローンと依存関係のインストール

GitHubから直接ソースリポジトリをクローンすることができます:

```
git clone https://github.com/node-red/node-red.git
```

これは現在のディレクトリに、
`node-red`というプロジェクトの全ソースコードを含んだディレクトリを作成します。
以下の残りの指示はこのディレクトリ内にいることを前提にします。

ビルドしたいブランチを選ぶ必要があります。

 - `master` - デフォルトのブランチ。これは現在の安定版リリースのコードに加え、
 次のメンテナンスリリースよりも先に適用した
 幾つかのバグフィックスを含んだメンテナンスブランチです。

 - `dev` - 開発ブランチ。これはすべての開発が進められるブランチです。

`dev`ブランチを利用したい場合、以下のコマンドを実行する必要があります:

```
git checkout dev
```

一度ブランチを選んだら、
以下のコマンドで全ての依存関係をインストールするべきです:

```
npm install
```

### Node-REDをビルドする

Node-REDを起動する前にビルドが必要です。これは以下のコマンドによって実行されます:

```
grunt build
```

### Node-REDを実行する

そして、以下のコマンドでNode-REDを実行することができます:

```
npm start
```

何かしらの[コマンドライン引数](local#コマンドラインの使い方)を渡したい場合、
以下のシンタックスを使う必要があります:

```
npm start -- <args>
```

引数`--`は`npm`に対して追加引数を実行時のコマンドに渡すことを指示します。

### 自動的に再起動する

ソースコードを編集した場合、Node-REDを再起動して変更をロードする必要があります。

これを自動的におこなうために特殊な`grunt`タスクが提供されています。

```
grunt dev
```

このコマンドはNode-REDをビルドして実行し、そしてソースコードへの変更がないかファイルシステムを監視を実施します。
エディタを構築するコードへの変更が検出された場合、
エディタコンポーネントをリビルドし、変更を確認するためにエディタをリロードします。
ランタイムまたはノードに加えられた変更を検出した場合、
これらの変更をロードするためにNode-REDを再起動します。

このモードは異なるフローファイルを指定する以外の引数を
Node-REDコマンドに対して渡すことを許可しません。

```
grunt dev --flowFile=my-flow-file.json
```