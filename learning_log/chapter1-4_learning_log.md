# Chapter 1–4 学習ログ：Git初期設定とローカル起点のリモート接続（改善版）

## 概要
Gitの初期設定からローカルリポジトリの作成、GitHubとの接続までを実施した。  
教科書では「fork → clone」によるリモート起点の方法が採用されていたが、今回はあえて

- ローカルでプロジェクト作成
- 後からGitHubに接続

という手順を取った。

その結果、

→「Gitは最初からGitHubとつながっているものではない」  
→「ローカルとリモートは完全に別物」

という点を実感として理解できた。

---

## ■ Git準備（環境構築）

### 実施内容

- Gitをインストール
- VS Codeをインストール
- Finderで拡張子表示を有効化

---

### 学び（具体）

- `.gitignore` を作成した際、最初は **.txtが付いてしまい認識されなかった**
- 拡張子を表示していなかったことが原因

→ GUI上では同じに見えても、実際は  
- `.gitignore.txt`（ただのテキスト）  
- `.gitignore`（Git設定ファイル）  
は完全に別物

→ **ファイル名の正確性はGit操作に直結する**

---

## ■ Gitの初期設定

### 実施内容

```bash
git config --global user.name "ユーザー名"
git config --global user.email "メールアドレス"
git config --global core.editor "code --wait"
git config --global init.defaultBranch main

---

### 学び（取捨選択）

- `core.editor` 未設定だとコミット時にエディタが開かず操作が止まる可能性がある
- VS Code連携によりコミットメッセージ編集がスムーズになった

→ **設定しないと実際に詰まるポイントがある**

---

## ■ ローカルリポジトリ作成

### 実施内容

    mkdir git-relearning-log
    cd git-relearning-log
    git init

---

### 学び（具体）

- `git init` 前：ただのフォルダ  
- `git init` 後：`.git` フォルダが生成されGit管理対象になる

→ この時点ではGitHubとは一切接続されていない
→ **GitとGitHubは別物であると実感**

---

## ■ add / commit の理解

### 実施内容

    git add npb_MEMO.md
    git commit -m "Create npb_MEMO.md"

---

### 学び（具体）

- `git status` を確認することで状態遷移を理解

    untracked → staged → committed

→ add = ステージング  
→ commit = 履歴確定  

→ **変更＝即保存ではない点がGitの特徴**

---

## ■ .gitignoreの導入

### 実施内容

`.gitignore` を作成

---

### 発生した問題

- `.gitignore.txt`として作成してしまった
- `git rm`が使えなかった

---

### 原因

- ファイルが untracked 状態だった
- Gitは未管理ファイルに対して `git rm` を使えない

---

### 学び（重要）

- Gitには2つの状態がある  
  - tracked（管理対象）  
  - untracked（未管理）

👉 **操作できるかどうかは状態に依存する**

---

## ■ GitHubとの接続

### 実施内容

    git remote add origin <URL>
    git push origin main

---

## ■ 発生した問題①：origin未設定

### 現象

    fatal: 'origin' does not appear to be a git repository

---

### 原因

- `git remote add` を実行していなかった

---

### 学び

→ `origin` は特別なものではなく単なるリモート名  
→ **Gitは自動で接続されるものではない**

---

## ■ 発生した問題②：Repository not found

### 原因

- GitHub上にリポジトリが存在していなかった
- GitHubにも同名のリポジトリを宣言して初めてpushできる

---

### 学び

→ ローカルとリモートは独立して存在する  
→ **存在場所が違うという概念を理解**

---

## ■ 発生した問題③：SSHパスミス

### 現象

    No such file or directory

---

### 原因

- Git Bashのパスを誤認  
  `/c/Users/git-relearning-log/...` と入力

---

### 正解

    /c/Users/liuni/...

---

### 学び

- Git BashはLinux風パス
- Windowsとは異なるパス体系

→ **環境ごとの差を理解**

---

## ■ 教科書との違い（重要）

### 教科書（リモート起点）

- fork → clone
- origin自動設定

---

### 今回（ローカル起点）

- git init → remote add → push
- 手動接続

---

### 本質理解

- clone =  
  → `remote add + fetch + checkout` のまとめ

→ **便利コマンドであり本質ではない**

---

## ■ 今回の本質理解（重要）

- Gitはローカル単体で完結するツール
- GitHubは後から接続する外部サービス

→ **最初からつながっているわけではない**

---

## ■ 追加の気づき

### エラーは理解の入り口

発生したエラー：

- origin未設定
- repository not found
- パスミス

→ すべて構造理解で解決できた

---

### Gitは状態を管理するツール

- untracked
- staged
- committed

→ **ファイルではなく状態を操作している**

---

## ■ 次のステップ

- HTML / CSSファイルの作成
- ブランチ運用
- GitHub PRフロー再現
