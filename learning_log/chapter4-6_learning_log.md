# Chapter 4–6 Learning Log: GitHub Flow

## 概要
GitHub Flow（fork・branch・pull request）の一連の流れを実践し、  
特に「ローカル・fork・本体リポジトリの関係」と「変更の流れ」を理解した。

---

## ■ 設計の考え方

今回の構成では、

- Sub：本体（upstream）
- Main：fork（origin）
- Local：作業環境

という3層構造で進んだ。

最初は単純に「GitHubにpushしている」と考えていたが、  
実際には

ローカル → fork → 本体

という段階的な流れになっていることが分かった。

---

## ■ 気づき・ミス

### ● originとupstreamの混乱

最初に混乱したのはここ：

- origin = 自分のリポジトリ
- upstream = 本体

という関係

#### 原因
- cloneした時点でoriginが設定されるため、「それがすべて」と思っていた

#### 修正
- fork構成ではリモートが複数存在する
- それぞれ役割が違う

と整理したことで理解できた

---

### ● pull origin mainでは更新されない理由

直感では：

git pull origin main

で最新になると思っていた

しかし実際は：

→ fork（origin）は古いまま

#### 原因
- マージされるのは本体（upstream）のみ

#### 修正
- upstreamから取得する必要がある

git pull upstream main

---

### ● GitHubのレビューの意味

最初は単なる確認作業だと思っていたが、

- 修正要求が来る
- 再度pushするとPRが更新される

という流れを体験して、

→ 「レビュー前提の開発プロセス」

であることを理解した

---

## ■ 学び

- GitHub Flowは単なるGit操作ではなく「開発プロセス」
- ブランチは作業の単位
- プルリクエストは変更の単位
- originとupstreamは役割が異なる
- fork構成では同期が明示的に必要

---

## ■ 今回の本質理解

GitHub Flowの本質は：

→ 変更を直接反映するのではなく、段階的に統合すること

- ローカルで変更
- ブランチで管理
- PRでレビュー
- mainに統合

この流れにより、安全に変更を取り込むことができる
