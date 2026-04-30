# Chapter 6 Summary: 複数ブランチの並行運用

## 概要
本章では、複数のブランチを同時に扱いながら開発を進める手順を確認した。  
一部の作業を途中で中断しつつ、別の作業を先に完了・マージし、その後に元の作業を再開する流れを実践した。

---

## ■ 前提構成

- upstream：本体リポジトリ（管理者）
- origin：forkしたリポジトリ（編集者）
- local：作業環境

---

## ■ シナリオ

2つの作業を別ブランチで管理する

- update-season-batting-stats  
  → 打撃成績の拡張（途中で中断して後で再開）

- update-postseason-result  
  → 試合結果の修正（先に完了・マージ）

---

## ■ 全体の流れ

### ① ブランチA作成（途中作業）

    git switch -c update-season-batting-stats

- 打撃成績の構造を変更（守備位置列追加、選手追加）
- 一部データは未入力のまま作業を中断

---

### ② コミット・プッシュ（途中状態で保存）

    git add .
    git commit -m "Update batting structure"
    git push origin update-season-batting-stats

---

### ③ mainに戻る（重要）

別ブランチを作る前にmainへ戻る

    git switch main

---

### ④ ブランチB作成（別作業）

    git switch -c update-postseason-result

- 試合結果をスコア形式に修正

---

### ⑤ コミット・プッシュ

    git add .
    git commit -m "Update postseason results"
    git push origin update-postseason-result

---

### ⑥ プルリクエスト作成・マージ

- GitHub上でPull Request作成
- 管理者がレビュー後マージ

---

### ⑦ 本体の最新状態を取得

    git switch main
    git pull upstream main

---

### ⑧ ブランチAに戻る

    git switch update-season-batting-stats

---

### ⑨ mainの変更を取り込む

    git merge main

---

### ⑩ 作業再開（未完部分を完成）

- 打撃成績をすべて入力

---

### ⑪ コミット・プッシュ

    git add .
    git commit -m "Complete batting stats"
    git push origin update-season-batting-stats

---

### ⑫ プルリクエスト作成・マージ

- GitHub上でPull Request作成
- 管理者がマージ

---

## ■ 本質

- 複数の作業はブランチで分離して管理する
- 作業は途中でもコミット・プッシュして保存できる
- 別ブランチの変更はmain経由で取り込む必要がある
- ブランチ作成時は必ず起点（main）を意識する

---

## ■ 重要なポイント

- mainに戻らずにブランチを作ると、意図しない依存関係が発生する
- 並行作業では「どのブランチがどの状態を基準にしているか」を常に意識する
- upstreamの更新は自動反映されないため、手動で取り込む必要がある
