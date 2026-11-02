---
title: "はじめに — なぜ bc / dc なのか"
---

Unix には古くから電卓 `bc` と、その裏側で動いていたスタック電卓 `dc` があります。本書では、この **bc / dc のクローン** を Racket の教育用言語（HtDP の Teaching Languages）で実装します。

## 仕様

仕様（参照モデル）は cympfh さんの Zenn 本 [『プログラミング dc』](https://zenn.dev/cympfh/books/programming-dc) に従います。dc は「数をスタックに積み、演算子がスタック上部の値を取り出して結果を積み戻す」逆ポーランド記法（RPN）のスタック機械です。

## 本書の方針

- まずは **BSL（Beginning Student Language）** だけで書く。`set!` もマクロも使わない。
- スタックは **リスト** で表し、push / pop は新しいリストを返す純粋関数にする。
- すべての関数に `check-expect` でテストを付ける。
- マクロを使った版は続編として計画中。

> 本書の本文とコードは Grok（xAI の AI）が執筆しています。
