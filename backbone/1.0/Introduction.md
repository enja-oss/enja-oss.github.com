---
title: Introduction.md
repository: backbone
branch: '1.0'
layout: default
---

+  元文書: [backbone/index.html at 9890d49db164e63b9b56e9d664ec0aab2289e0de · documentcloud/backbone · GitHub](https://github.com/documentcloud/backbone/blob/9890d49db164e63b9b56e9d664ec0aab2289e0de/index.html "backbone/index.html at 9890d49db164e63b9b56e9d664ec0aab2289e0de · documentcloud/backbone · GitHub")

##イントロダクション

大量のJavaScriptを含むWebアプリケーションの開発において、まず最初に学ぶ事はデータをDOMに紐付けるのをやめることです。HTMLのUI、JavaScriptのロジック、そしてサーバ上のデータベース、これらの間でデータの同期を取ろうとして、jQueryのセレクタとコールバックが複雑に積み重なったJavaScriptアプリを書いてしまう、というのは非常にやってしまいがちなことですが、リッチなクライアントサイド・アプリケーションにおいては、より構造的なアプローチの方がうまくいく場合が多いのです。

Backboneではデータをモデルとして表現します。モデルは生成、評価、破棄することが可能で、さらにサーバに保存できます。UI操作によりモデルの属性が変更された場合、changeイベントが発行されます。イベントはモデルの状態を表示しているすべてのビューに通知され、ビューはそのイベントに反応し、新しい情報を表示するために自身を再描画します。Backboneを使って書かれたアプリでは、DOMの中から特定のidを持つエレメントを検索したり、手動でHTMLを更新したりといった、つなぎのコードは不要です。モデルが変更された際に、ビューは単に自分自身を更新します。 

はじめての方で、Backboneが何のためのものなのかよくわからない方は、[Backbone使ったプロジェクトのリスト](http://backbonejs.org/#examples)を見るところから初めてください。

以下に登場するコード例の多くは実際に動かしてみることができます。動かすには再生ボタンを押してください。 
