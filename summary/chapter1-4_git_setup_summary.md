# Chapter 1–4 Summary: Git & GitHub Setup (Local-first Workflow)

## 概要
GitとGitHubを使った開発の初期構築を行った。  
今回はローカルでプロジェクトを作成してからGitHubに接続する「ローカル起点」の流れを採用し、基本的なGit操作とリモート連携を整理した。
なお、すでにgit-learning-logのリポジトリで学んでいるので重要でない部分の詳細は割愛する

---

## ■ ① 開発環境の準備

GitとVS Codeをインストールし、ファイルの拡張子が表示されるように設定した。  
拡張子の表示は、ファイルの見え方がGUIとCUIで同じになるようにするためである。

---

## ■ ② Gitの初期設定

git config --global user.name "ユーザー名"  
→ コミット時の名前を設定
今回は
管理者がmawsonlakes790913-sub
編集者がmawsonlakes790913
である

git config --global user.email "メールアドレス"  
→ コミット時のメールアドレスを設定

git config --global core.editor "code --wait"  
→ エディターをVS Codeに設定

git config --global init.defaultBranch main  
→ デフォルトブランチを main に統一

---

## ■ ③ ローカルリポジトリの作成

mkdir npb  
→ 作業用ディレクトリを作成

cd npb  
→ 作業ディレクトリへ移動

git init  
→ ローカルリポジトリを初期化

---

## ■ ④ ファイルの管理とコミット

git add npb_MEMO.md  
→ (動作確認用の空の)ファイルをステージングエリアに登録

git commit -m "Create npb_MEMO.md"  
→ 変更内容を履歴として記録

---

## ■ ⑤ .gitignoreの設定

touch .gitignore  
→ 管理対象外ファイルを指定する設定ファイルを作成

git add .gitignore  
git commit -m "Add .gitignore"  
→ 設定をリポジトリに反映

---

## ■ ⑥ GitHubとの接続

git remote add origin <URL>  
→ ローカルとGitHubリポジトリを接続

git push -u origin main  
→ ローカルの内容をリモートへ反映

---

## ■ 教科書との違い（重要）

教科書では fork と git clone を使用するため、clone時点で origin が自動設定される。  
一方今回は、ローカルで先に作成したため、手動で remote を追加している。

この違いはコマンドではなく、

- リモート起点（clone）
- ローカル起点（remote add）

という構造の違いによるものである。

---

## ■ 学び・気づき

- Gitはローカルとリモートが独立した存在である
- 両者は明示的に接続しないと連携しない
- remote addは手動で接続を定義する操作である

---

## ■ 今回の本質理解

Gitの初期構築は以下の流れで成立する：

1. ローカル環境の準備（config / init）
2. ファイルの履歴管理（add / commit）
3. リモートとの接続（remote add / push）

この構造を理解することで、Git操作を手順ではなく仕組みとして扱えるようになる。
