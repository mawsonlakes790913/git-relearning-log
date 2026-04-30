# Chapter 4–5 Summary: GitHub Flow（Fork → Branch → PR）

## 概要
本章では、forkを起点としたGitHub Flowを実践した。  
管理者（Sub）のリポジトリを編集者（Main）がforkし、ローカルで作業後、Pull Requestを通じて変更を本体に反映する流れを確認した。

---

## ■ 前提構成

- Sub：本体リポジトリ（upstream）
- Main：forkしたリポジトリ（origin）
- Local：作業環境

fork構成のため、変更はupstreamに反映され、originは自動更新されない。

---

## ■ 全体の流れ

### ① fork → clone（作業開始）

GitHub上でfork後、ローカルに取得

    git clone git@github.com:<ユーザー名>/git-relearning-log.git
    cd git-relearning-log

---

### ② ブランチ作成・切り替え

作業用ブランチを作成

    git switch -c update-batting-stats

---

### ③ 編集・差分確認

ローカルでファイルを編集後、差分を確認

    git diff main

---

### ④ コミット・プッシュ

変更をコミットし、forkに反映

    git add .
    git commit -m "Update batting stats"
    git push origin update-batting-stats

---

### ⑤ プルリクエスト作成（GitHub上）

GitHub上で以下を実施

- Compare & pull request を選択
- Pull Requestを作成

---

### ⑥ レビュー対応 → 再プッシュ

レビュー指摘を反映し、同じブランチに再度push

    git add .
    git commit -m "Fix styling and highlight stats"
    git push origin update-batting-stats

---

### ⑦ mainへマージ（管理者）

GitHub上で管理者がPull Requestをマージ

---

### ⑧ 最新状態の同期（forkの更新）

forkは自動更新されないため、本体から同期する

    git switch main
    git remote add upstream git@github.com:<管理者>/git-relearning-log.git
    git pull upstream main
    git push origin main

---

## ■ 本質

- 作業はmainではなくブランチで行う
- Pull Requestで変更を提案し、レビューを経て統合する
- fork構成では upstream → local → origin の順で同期が必要
