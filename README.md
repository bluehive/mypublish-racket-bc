# mypublish-racket-bc

**Racket でつくる bc** — Unix の電卓 `bc` / `dc` のクローンを Racket の教育用言語で実装する Zenn 本のリポジトリです。

> ✍️ **初稿の本文・サンプルコードは Grok（xAI の AI、Grok Bot）、続編原稿と編集計画は Codex が執筆しています。** 企画・監修は bluehive。

## 目的

- Zenn の本（`books/racket-bc/`）として公開し、同じ原稿から EPUB も生成する（Zenn → EPUB）。
- **仕様**は cympfh さんの Zenn 本 [『dcがいかに素敵なプログラミング言語であるか伝えたい』](https://zenn.dev/cympfh/books/programming-dc) に従う。dc のスタック機械（数を積み、演算子がスタック上部を取り出して結果を積み戻す RPN）をモデルにする。
- 姉妹リポジトリ: [mypublish-racket-turtle](https://github.com/bluehive/mypublish-racket-turtle)

## 言語計画

| 版 | 言語 | 状態 | 内容 |
|---|---|---|---|
| BSL 版 | `#lang htdp/bsl` | **執筆中（今ここ）** | リストによる関数型スタック、四則演算、`p` 表示。`set!`・マクロなし |
| マクロ版 | `#lang racket`（`define-syntax`） | 構想中 | dc 風の記法を Racket に埋め込む |

### BSL 版で扱う dc サブセット

数（push）、`+` `-` `*` `/`、`p`（トップ表示）、`d`（複製）、`r`（交換）、`c`（全消去）。トークンのリストを入力とし、GNU bc の完全な文法は扱いません。

## 目次（Zenn book）

1. [はじめに](books/racket-bc/intro.md)
2. [第1章 BSL でスタックをつくる](books/racket-bc/ch01-bsl-stack.md)
3. [第2章 BSL で四則演算と表示](books/racket-bc/ch02-bsl-arith.md)
4. [第3章 トークン列を再帰で実行する](books/racket-bc/ch03-bsl-run.md)
5. [おわりに](books/racket-bc/closing.md)

## フォルダ構成

```
books/racket-bc/        Zenn book 原稿（正本）と config.yaml
code/                   BSL ソース（racket で実行・check-expect テスト）
drafts/racket-bc/       下書き
manuscript/racket-bc/   EPUB 用に結合した book.md（生成物）
scripts/racket-bc/      結合・EPUB ビルド・検証スクリプト
assets/epub/            EPUB 用 CSS（横書き／縦書き）
output/racket-bc/       EPUB 出力先
notes/  articles/  images/
.github/ISSUE_TEMPLATE/
```

## セットアップ

```sh
npm i                 # zenn-cli
mise install          # node, watchexec
# Racket 8.x を別途インストール（racket コマンドが PATH にあること）
```

## タスク（mise）

| タスク | 内容 |
|---|---|
| `mise run zenn:preview` | Zenn プレビュー（localhost:8000） |
| `mise run test:racket` | `code/*.rkt` を実行し check-expect を検証 |
| `mise run ci:test` | ローカル CI ゲート |
| `mise run watch:test` | `code/` 変更で自動テスト |
| `mise run book:combine` | 章を `manuscript/racket-bc/book.md` に結合 |
| `mise run book:epub` | 横書き EPUB（要 pandoc） |

## ライセンス

[BSD 2-Clause License](LICENSE)

## 編集計画

現状分析・章構成案・承認対象は [続編執筆計画](notes/continuation-plan.md) を参照してください。
