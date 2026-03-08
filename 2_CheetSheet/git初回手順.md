# git初回手順

- [git初回手順](#git初回手順)
  - [1. 作業フォルダをGitリポジトリとして初期化](#1-作業フォルダをgitリポジトリとして初期化)
  - [2. 追跡するファイルをステージング](#2-追跡するファイルをステージング)
    - [全ファイルを追加](#全ファイルを追加)
    - [個別ファイル](#個別ファイル)
  - [3. コミット](#3-コミット)
  - [4. GitHubでリポジトリ作成](#4-githubでリポジトリ作成)
  - [5. リモートリポジトリ登録](#5-リモートリポジトリ登録)
  - [6. ブランチ名をmainに変更](#6-ブランチ名をmainに変更)
  - [7. GitHubへ送信（push）](#7-githubへ送信push)
  - [全体の流れ](#全体の流れ)

---

## 1. 作業フォルダをGitリポジトリとして初期化

`git init`

---

## 2. 追跡するファイルをステージング

### 全ファイルを追加

`git add .`

### 個別ファイル

`git add ファイル名`

---

## 3. コミット

`git commit -m "first commit"`

---

## 4. GitHubでリポジトリ作成

GitHubでNew repositoryを作成

例：
https://github.com/ユーザー名/リポジトリ名.git

---

## 5. リモートリポジトリ登録

`git remote add origin https://github.com/ユーザー名/リポジトリ名.git`

origin = リモートリポジトリの名前（慣例）

確認：
`git remote -v`

---

## 6. ブランチ名をmainに変更

`git branch -M main`

最近のGitHubは`master`よりも `main` が標準。

---

## 7. GitHubへ送信（push）

`git push -u origin main`

意味：
origin = GitHub
main   = ブランチ
-u     = 今後 push を簡略化

以後は`git push`だけで送信可能

---

## 全体の流れ

```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/ユーザー名/リポジトリ名.git
git push -u origin main
```