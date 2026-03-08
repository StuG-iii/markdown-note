# GitHub リモートリポジトリとのやり取り

## リモートを表示する

`git remote`

### 対応するURLを表示

`git remote -v`

## リモートリポジトリからローカルリポジトリへ情報を取得（fetch）

`git fetch <リモート名>`
`git fetch origin`

## fetchした内容をローカルに反映

`git merge`

## リモートリポジトリからローカルリポジトリへ情報を取得してマージする

`git pull <リモート名> <ブランチ名>`
`git pull origin master`

### 上記コマンドは省略可能

`git pull`

### これは下記コマンドと同じこと

`git fetch origin master`
`git merge origin/master`

### 注意点

取得した情報は**今いるブランチに反映される**ため注意が必要
基本pullを使わずfetch + mergeを使う。
masterブランチにいる時が分かっている時のみpullを利用。

## リモートの詳細情報表示する

`git remote show <リモート名>`
`git remote show origin`

## リモート名を変更・削除

### 変更

`git remote rename <旧リモート名> <新リモート名>`
`git remote rename tutorial new_tutorial`

### 削除

`git remote rm <リモート名>`
`git remote rm new_tutorial`