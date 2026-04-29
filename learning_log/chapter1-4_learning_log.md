```markdown
# Chapter 1–4 学習ログ：Git初期設定とローカル起点のリモート接続

## 概要
Gitの初期設定からローカルリポジトリの作成、GitHubとの接続までを一通り実施した。  
今回は教科書とは異なり、ローカルでプロジェクトを作成してからリモートに接続する方法を採用し、その違いを検証しながら進めたことで、Gitの構造理解が深まった。

---

## ■ Git準備（環境構築）

### 実施内容

- WindowsにGitをインストール
- VS Codeをインストール
- エクスプローラーで拡張子を表示

---

### 学び

- 拡張子の非表示は .gitignore や設定ファイルの扱いでミスの原因になる
- 開発環境の設定は後のトラブル回避に直結する

---

## ■ Gitの初期設定

### 実施内容

git config --global user.name "ユーザー名"  
git config --global user.email "メールアドレス"  
git config --global core.editor "code --wait"  
git config --global init.defaultBranch main  

---

### 学び

- user.name / user.email はコミット履歴に残る重要情報
- エディター設定をしておかないと操作が不便になる
- デフォルトブランチの統一はチーム開発で重要

---

## ■ ローカルリポジトリ作成

### 実施内容

mkdir git-relearning-log
cd git-relearning-log  
git init  

また、挙動確認用として npb_MEMO.md を作成

---

### 学び

- Gitはディレクトリ単位で管理される
- git init により「履歴管理が開始される」状態になる

---

## ■ add / commit の理解

### 実施内容

git add npb_MEMO.md  
git commit -m "Create npb_MEMO.md"  

---

### 学び

- add は「変更を記録対象にする操作」
- commit は「履歴として確定する操作」
- この2段階構造がGitの基本

---

## ■ .gitignoreの導入

### 実施内容

.gitignore を作成しコミット

---

### 発生した問題

- gitignore（ドットなし）で作成してしまった
- git rm が使えず削除に戸惑った

---

### 原因

- Gitは未追跡ファイルを管理していないため git rm が使えない
- .gitignore は「.」が必須

---

### 学び

- tracked / untracked の違いを理解できた
- ファイル名の正確性が重要

---

## ■ GitHubとの接続

### 実施内容

1. GitHubにリポジトリ作成  
2. SSH設定（公開鍵登録）  
3. 接続とpush

git remote add origin <URL>  
git push origin main  

---

## ■ 発生した問題①：origin未設定

### 現象

fatal: 'origin' does not appear to be a git repository  

---

### 原因

- リモート未設定

---

### 解決

git remote add origin <URL>  

---

## ■ 発生した問題②：Repository not found

### 現象

ERROR: Repository not found  

---

### 原因

- GitHub側にリポジトリが存在しなかった

---

### 解決

- GitHubでリポジトリ作成後に再push

---

## ■ 発生した問題③：SSHパスミス

### 現象

No such file or directory  

---

### 原因

- /c/Users/git-relearning-log/... のように誤ったパス指定
- 正しくは /c/Users/liuni/...

---

### 学び

- Git BashのパスとWindowsの実パスの対応を理解した

---

## ■ 教科書との違い（重要）

### 教科書

- fork → git clone
- origin自動設定
- リモート起点

---

### 今回

- git init → remote add → push
- 手動で接続
- ローカル起点

---

### 本質

違いはコマンドではなく：

- リモート起点（clone）
- ローカル起点（remote add）

という構造の違い

---

## ■ 今回の本質理解

- Gitはローカルとリモートが独立している
- 接続は明示的に行う必要がある
- cloneはremote addを含んだコマンドである

---

## ■ 追加の学び・気づき

### エラーは理解の入り口

- origin未設定
- repository not found
- パスミス

👉 すべて構造理解で解決可能

---

### Gitは状態管理のツール

- 何が管理されているか（tracked）
- 何が未管理か（untracked）

👉 状態を意識することが重要

---

### ローカル起点の重要性

- 個人開発ではこちらが基本
- ポートフォリオ作成にも直結

---

## ■ 次のステップ

- HTML / CSSファイルの作成
- 複数ブランチでの編集
- GitHubでのPRフロー再現
```
