# Scratch経験者向け改稿の範囲と検証

確認日: 2026-11-03（JST）。読者: Scratchを数時間操作した高校生。Racket、関数、リスト、テストの事前知識は前提としない。

## 変更範囲

`books/` 以下の本文全5ファイルとconfigの紹介文を改稿した。既存の `code/*.rkt` の動作は変更していない。

- はじめに: DrRacketの導入、#langを使う言語設定、定義／対話エリア、Run、かっこの式、試す場所、失敗時の対処。
- 第1章: 皿の山によるスタックの導入、リストと空リスト、first・rest・cons、check-expectの実際と予想、意図的な失敗と復帰、define、引数と戻り値、if・empty?・check-error、push/top/pop/d/r/cの説明。
- 第2章: 四則演算の入力順、cond・string=?・else、binopを部分式に分けた説明、数の不足とゼロ除算、分数、出力との接続。
- 第3章: 入力・スタック・出力の区別、stepの全定義、再帰を表で導入、停止条件、runの読み方、異なる出力値による順番の確認。
- おわりに: 復習表、追加問題、未実装の範囲、次の学習課題。

## 技術上の判断

- 本文のtop/popとbinopは既存codeの定義とそろえた。top/popの空入力は明示的な `stack empty` エラー。
- apply-opは四つの演算子のみを渡す既存の前提を明記。elseを未知記号の拒否だと説明しない。stepが既知の演算子を選んでから呼ぶ。
- runの戻り値はpで記録した出力リストであり、最終スタックでも逐次印字でもない。
- 未説明だったsecondは使わず、既存codeと同じtop/popで二番目を読む。
- 別エージェントの司書ペルソナ評価は [評価レポート](beginner-librarian-review.md) を参照。実在の司書や実際の高校生のユーザーテストではない。

## 実行検証

Racket v8.10 [cs] で実施。

| 対象 | 方法 | 結果 |
|---|---|---|
| 既存code/ch01-stack.rkt | `racket code/ch01-stack.rkt` | 7 tests passed |
| 既存code/ch02-arith.rkt | `racket code/ch02-arith.rkt` | 11 tests passed |
| 第1章のracketブロック | BSLヘッダ・requireの下へ、登場順に定義とテストを置き、末尾でtest | 14 tests passed |
| 第2章の例 | 完成ch02コードへ本文のテストを追加、定義を重複させず実行 | 22 tests passed |
| 第3章の例 | 同上。入力リストの例も実行 | 25 tests passed |
| おわりにの追加問題 | 完成ch02コードへ追加して実行 | 12 tests passed |
| はじめにの初回プログラム | #langからtestまで独立実行 | The test passed |
| はじめにの完成例 | runを含む先取り例を完成ch02コードとともに実行 | `(list 5)`相当の値、既存11 tests passed |

章ごとの件数には既存テストや他章と同じテストを含む。これらの合計を固有のテスト件数とは扱わない。初回の抽出スクリプトでは、introの先取り例を#langより先に連結して実行に失敗したため、本文どおり初回プログラムと完成例の文脈を分離して再実行し、上記を確認した。これは本文コードの失敗ではない。

- `python3 scripts/racket-bc/combine_drafts.py`: 全5本文の結合成功。
- configの章一覧・各ファイルのfront matter・コードフェンスの対応・GitHubリポジトリ内ファイルリンク: 確認成功。
- `git diff --check`: 成功。
- DrRacketのGUI操作と、実際の高校生が独力で学べるかの観察、Zennブラウザ表示は未実施。Racket実行の成功だけで、それらも検証済みとはしない。

## 出版工程の残課題

`python3 scripts/racket-bc/build.py --format epub-horizontal --no-cover --verify` は、EPUB生成後に `AssertionError: nav entries missing` で失敗した。`build_epub.py` が本書にない「序章」を目次に要求する、既知の条件不一致を再確認した。付録などを要求する条件も以前から残っている。本文の学習手順とは分け、既存の出版工程の残課題として管理する。今回の目的はbooksの入門者向け改稿とレビュー用PRであり、公開・配布用EPUBの完成を含めない。生成したbook.mdとEPUBは確認用で、今回のコミットには加えない。

## 仕様の参照

- [BSL公式仕様](https://docs.racket-lang.org/htdp-langs/beginner.html)
- [DrRacket画面とRunの公式説明](https://docs.racket-lang.org/drracket/interface-essentials.html)
- [Racketダウンロード](https://download.racket-lang.org/)
