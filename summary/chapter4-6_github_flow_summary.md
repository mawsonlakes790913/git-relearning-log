# Chapter 4–6 Summary: GitHub Flow (Fork → Branch → PR)

## 概要
本章では、GitHubを用いた基本的な開発フロー（GitHub Flow）を実践した。  
本体リポジトリ（Sub）をforkし、作業者（Main）がローカルで変更を行い、プルリクエストを通じて変更を統合する流れを確認した。

---

## ■ 前提構成

- Sub：本体リポジトリ（upstream）
- Main：forkしたリポジトリ（origin）

fork構成のため、変更は本体（upstream）にマージされ、fork（origin）は自動では更新されない。

---

## ■ 全体の流れ

### ① fork → clone（作業開始）

git clone <URL>  
cd リポジトリ名  

---

### ② ブランチ作成・切り替え

git switch -c ブランチ名  

---

### ③ 編集・差分確認

git diff main  

---

### ④ コミット・プッシュ

git add .  
git commit -m "message"  
git push origin ブランチ名  

---

### ⑤ プルリクエスト作成（GitHub上）

Compare & pull request → 作成  

---

### ⑥ レビュー対応 → 再プッシュ

（修正後）

git add .  
git commit -m "fix"  
git push origin ブランチ名  

---

### ⑦ mainへマージ（管理者）

GitHub上でMerge  

---

### ⑧ 最新状態の同期（重要）

git switch main  
git remote add upstream <本体URL>  
git pull upstream main  
git push origin main  

---

## ■ 本質

- 開発はmainではなくブランチで行う  
- プルリクエストでレビューと統合を行う  
- fork構成では upstream → origin の同期が必要  
