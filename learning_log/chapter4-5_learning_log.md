# Chapter 4–5 学習ログ：Fork・ブランチ運用とPull Requestフロー

## 概要
本章では、GitHub Flow（fork → branch → pull request → merge）を実際に再現した。  
管理者（Sub）と編集者（Main）という2つの役割を1人で再現しながら、

- ローカル、リモート、他人のリポジトリの関係
- Pull Request後にforkが自動更新されない理由

を実体験として理解した。

---

## ■ Chapter 4：ForkとClone（作業開始）

### 実施内容

- 管理者（Sub）がWebページを作成しリモートへpush
- 編集者（Main）が以下を実施
  1. GitHub上でfork
  2. forkしたリポジトリをローカルにclone

---

### 学び（具体）

#### forkの本質

- forkは単なるコピーではなく、独立した別リポジトリとして扱われる
- upstream（本体）とorigin（自分のfork）は別の存在

そのため、片方を更新してももう一方には自動で反映されない

---

#### cloneの理解

- cloneを実行するとoriginが自動で設定される
- ローカルと自分のリモートは接続されるが、本体（upstream）とは接続されていない

---

### 気づき

- Chapter1〜3で行ったremote addと異なり、cloneは接続設定を含むコマンド
- ただし接続されるのはfork先であり、本体ではない

---

## ■ Chapter 5：ブランチ運用とPull Request

## ● 目的

- HTMLファイルに選手成績を追加する
- ブランチを用いて安全に変更を行う

---

## ■ ブランチ作成と編集

### 実施内容

    git branch update-batting-stats
    git switch update-batting-stats

- index.htmlを編集し、タイロン・ウッズの成績を追加

---

### 学び（具体）

- mainブランチではなく別ブランチで作業することで、完成版に直接影響を与えない
- mainは安定した状態を保つためのブランチであり、変更はブランチ上で行う必要がある

---

## ■ 差分確認（git diff）

### 実施内容

    git diff main

---

### 学び

- 実際にどの行が変更されたかを確認できる
- 編集内容と実際の差分が一致しているかを確認することで、意図しない変更を防げる

---

## ■ pushとPull Request

### 実施内容

    git push origin update-batting-stats

- GitHub上でPull Requestを作成

---

### 学び

- pushだけではmainブランチは更新されない
- Pull Requestは変更内容を提案する段階であり、マージされて初めて反映される

---

## ■ レビューと再修正

### 実施内容

- 管理者がレビューを実施
- 以下の修正指示を受ける
  - タイロン・ウッズの本塁打数と打点を強調
  - 福留孝介の打率を太字に変更

- 編集者がローカルで修正し、再度push

---

### 学び（重要）

- Pull Requestは一度で完了するものではない
- 修正内容を反映して再度pushすることで、同じPull Request内で更新が可能

---

## ■ マージ

### 実施内容

- 管理者がGitHub上でmerge

---

### 学び

- マージされるのは本体（upstream）のみ
- fork（origin）は自動では更新されない

---

## ■ fork後の同期問題

### 発生した問題

- git pull origin main を実行しても最新状態にならない

---

### 原因

- originは自分のforkであり、本体ではない
- forkは自動同期されない

---

### 解決手順

    git switch main
    git remote add upstream <本体URL>
    git pull upstream main
    git push origin main

---

### 学び（本質）

- データは upstream → ローカル → origin の順に流れる
- originからpullしても本体の更新は取得できない

---

## ■ GitHub Flowの理解

実際に行った流れ：

1. fork
2. clone
3. ブランチ作成
4. 編集
5. push
6. Pull Request作成
7. レビュー
8. 修正と再push
9. merge
10. upstreamから同期

---

## ■ 重要な気づき

### 1. 人とリポジトリの区別が必要

- Sub（管理者）
- Main（編集者）

- upstream（本体）
- origin（自分のfork）
- local（作業環境）

これらを区別して考えないと混乱する

---

### 2. pullの誤解

- git pull origin main はforkの更新を取得するだけ
- 本体の変更は取得できない

---

### 3. Pull Requestの役割

- 単なるマージ手段ではない
- レビューと修正を含む開発プロセスの一部

---

## ■ 到達点

- GitHub Flowを一通り再現できた
- 今回は職務分掌を徹底したので前回のような混乱が起きることはなかった
- fork構成、ブランチ運用、Pull Request、同期の流れを理解した
- 操作だけでなく、リポジトリ間の関係を構造として理解できた
