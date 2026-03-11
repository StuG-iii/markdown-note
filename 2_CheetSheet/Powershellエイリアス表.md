# PowerShell エイリアス一覧と意味・cmd対比

- [PowerShell エイリアス一覧と意味・cmd対比](#powershell-エイリアス一覧と意味cmd対比)
  - [1. ファイル・ディレクトリ操作系](#1-ファイルディレクトリ操作系)
  - [2. パス・項目情報系](#2-パス項目情報系)
  - [3. テキスト・検索・表示系](#3-テキスト検索表示系)
  - [4. 履歴・画面・ヘルプ系](#4-履歴画面ヘルプ系)
  - [5. プロセス・サービス系](#5-プロセスサービス系)
  - [6. 変数・環境・実行系](#6-変数環境実行系)
  - [7. ネットワーク・ダウンロード系](#7-ネットワークダウンロード系)
  - [cmdとの違いが分かりにくいポイント](#cmdとの違いが分かりにくいポイント)
    - [`dir`](#dir)
    - [`type` / `cat`](#type--cat)
    - [`echo`](#echo)
    - [`set`](#set)
    - [`cd`](#cd)
  - [よく使う実践セット](#よく使う実践セット)
  - [エイリアス確認コマンド](#エイリアス確認コマンド)
  - [cmdユーザー向けの覚え方](#cmdユーザー向けの覚え方)
  - [実用例](#実用例)
    - [1MB超のファイルだけ表示](#1mb超のファイルだけ表示)
    - [txtファイルだけ表示](#txtファイルだけ表示)
    - [ファイル内容から "error" を検索](#ファイル内容から-error-を検索)
    - [メモ帳を終了](#メモ帳を終了)

## 1. ファイル・ディレクトリ操作系

| PowerShellエイリアス | 実体コマンド         | 意味                       | cmdで近いもの              |
| -------------------- | -------------------- | -------------------------- | -------------------------- |
| `dir`                | `Get-ChildItem`      | ファイル・フォルダ一覧表示 | `dir`                      |
| `ls`                 | `Get-ChildItem`      | 一覧表示（Unix風）         | `dir`                      |
| `gci`                | `Get-ChildItem`      | 一覧表示の短縮             | `dir`                      |
| `cd`                 | `Set-Location`       | ディレクトリ移動           | `cd`                       |
| `chdir`              | `Set-Location`       | ディレクトリ移動           | `cd`                       |
| `pwd`                | `Get-Location`       | 現在の場所表示             | `cd`                       |
| `gl`                 | `Get-Location`       | 現在位置の短縮             | `cd`                       |
| `md`                 | `mkdir` (`New-Item`) | フォルダ作成               | `mkdir`, `md`              |
| `mkdir`              | `New-Item`           | フォルダ作成               | `mkdir`, `md`              |
| `rd`                 | `Remove-Item`        | フォルダ削除               | `rmdir`, `rd`              |
| `rmdir`              | `Remove-Item`        | フォルダ削除               | `rmdir`, `rd`              |
| `del`                | `Remove-Item`        | ファイル削除               | `del`, `erase`             |
| `erase`              | `Remove-Item`        | ファイル削除               | `erase`, `del`             |
| `rm`                 | `Remove-Item`        | 削除（Unix風）             | `del`, `rmdir`             |
| `ri`                 | `Remove-Item`        | 削除の短縮                 | `del`, `rmdir`             |
| `copy`               | `Copy-Item`          | コピー                     | `copy`, `xcopy` の一部用途 |
| `cp`                 | `Copy-Item`          | コピー（Unix風）           | `copy`                     |
| `cpi`                | `Copy-Item`          | コピーの短縮               | `copy`                     |
| `move`               | `Move-Item`          | 移動・名前変更             | `move`                     |
| `mv`                 | `Move-Item`          | 移動（Unix風）             | `move`                     |
| `mi`                 | `Move-Item`          | 移動の短縮                 | `move`                     |
| `ren`                | `Rename-Item`        | 名前変更                   | `ren`, `rename`            |
| `rni`                | `Rename-Item`        | 名前変更の短縮             | `ren`                      |
| `type`               | `Get-Content`        | ファイル内容表示           | `type`                     |
| `gc`                 | `Get-Content`        | ファイル内容表示の短縮     | `type`                     |
| `cat`                | `Get-Content`        | ファイル内容表示（Unix風） | `type`                     |

---

## 2. パス・項目情報系

| PowerShellエイリアス | 実体コマンド       | 意味                         | cmdで近いもの         |
| -------------------- | ------------------ | ---------------------------- | --------------------- |
| `gi`                 | `Get-Item`         | ファイルやフォルダの情報取得 | 明確な対応なし        |
| `gp`                 | `Get-ItemProperty` | プロパティ取得               | 明確な対応なし        |
| `sp`                 | `Set-ItemProperty` | プロパティ設定               | 明確な対応なし        |
| `ni`                 | `New-Item`         | 新しい項目作成               | `md` に近いがより汎用 |
| `ii`                 | `Invoke-Item`      | 既定アプリで開く             | `start` に近い        |
| `start`              | `Start-Process`    | プログラム起動               | `start`               |

---

## 3. テキスト・検索・表示系

| PowerShellエイリアス | 実体コマンド     | 意味                           | cmdで近いもの                |
| -------------------- | ---------------- | ------------------------------ | ---------------------------- |
| `echo`               | `Write-Output`   | 文字列や値を出力               | `echo`                       |
| `write`              | `Write-Output`   | 出力                           | `echo`                       |
| `select`             | `Select-Object`  | 項目選択                       | 近いものなし                 |
| `sort`               | `Sort-Object`    | 並べ替え                       | `sort`                       |
| `where`              | `Where-Object`   | 条件で絞り込み                 | `find`, `findstr` の一部用途 |
| `?`                  | `Where-Object`   | 絞り込み短縮                   | `findstr` にやや近い         |
| `measure`            | `Measure-Object` | 件数・合計など集計             | 近いものなし                 |
| `group`              | `Group-Object`   | グループ化                     | 近いものなし                 |
| `ft`                 | `Format-Table`   | 表形式表示                     | 近いものなし                 |
| `fl`                 | `Format-List`    | リスト形式表示                 | 近いものなし                 |
| `fw`                 | `Format-Wide`    | 横並び表示                     | 近いものなし                 |
| `gm`                 | `Get-Member`     | オブジェクトの型・メンバー確認 | 近いものなし                 |
| `find`               | `Select-String`  | 文字列検索                     | `find`, `findstr`            |
| `sls`                | `Select-String`  | 文字列検索の短縮               | `findstr`                    |

---

## 4. 履歴・画面・ヘルプ系

| PowerShellエイリアス | 実体コマンド    | 意味                 | cmdで近いもの     |
| -------------------- | --------------- | -------------------- | ----------------- |
| `history`            | `Get-History`   | 実行履歴表示         | `doskey /history` |
| `h`                  | `Get-History`   | 履歴表示の短縮       | `doskey /history` |
| `clc`                | `Clear-Content` | 内容消去             | 対応薄い          |
| `clear`              | `Clear-Host`    | 画面クリア           | `cls`             |
| `cls`                | `Clear-Host`    | 画面クリア           | `cls`             |
| `help`               | `Get-Help`      | ヘルプ表示           | `help`            |
| `man`                | `Get-Help`      | ヘルプ表示（Unix風） | `help`            |

---

## 5. プロセス・サービス系

| PowerShellエイリアス | 実体コマンド    | 意味             | cmdで近いもの                  |
| -------------------- | --------------- | ---------------- | ------------------------------ |
| `ps`                 | `Get-Process`   | プロセス一覧     | `tasklist`                     |
| `gps`                | `Get-Process`   | プロセス一覧短縮 | `tasklist`                     |
| `kill`               | `Stop-Process`  | プロセス終了     | `taskkill`                     |
| `spps`               | `Stop-Process`  | プロセス停止短縮 | `taskkill`                     |
| `sasv`               | `Start-Service` | サービス開始     | `net start`                    |
| `spsv`               | `Stop-Service`  | サービス停止     | `net stop`                     |
| `gsv`                | `Get-Service`   | サービス一覧     | `sc query`, `net start` の一部 |

---

## 6. 変数・環境・実行系

| PowerShellエイリアス | 実体コマンド        | 意味                       | cmdで近いもの          |
| -------------------- | ------------------- | -------------------------- | ---------------------- |
| `set`                | `Set-Variable`      | 変数設定                   | `set`                  |
| `sv`                 | `Set-Variable`      | 変数設定短縮               | `set`                  |
| `gv`                 | `Get-Variable`      | 変数取得                   | `set` で一覧確認に近い |
| `env:`               | 環境変数ドライブ    | 環境変数アクセス           | `%PATH%` など          |
| `iex`                | `Invoke-Expression` | 文字列をコマンドとして実行 | 近いものなし           |
| `&`                  | 呼び出し演算子      | コマンドやスクリプト実行   | cmdに明確対応なし      |

---

## 7. ネットワーク・ダウンロード系

| PowerShellエイリアス | 実体コマンド                  | 意味             | cmdで近いもの |
| -------------------- | ----------------------------- | ---------------- | ------------- |
| `curl`               | `Invoke-WebRequest` ※環境依存 | Web取得          | `curl`        |
| `wget`               | `Invoke-WebRequest` ※環境依存 | Web取得          | 明確にはなし  |
| `iwr`                | `Invoke-WebRequest`           | HTTPリクエスト   | `curl`        |
| `irm`                | `Invoke-RestMethod`           | REST API向け取得 | `curl`        |

※Windows環境では `curl` が本物の `curl.exe` を指す場合もある。
PowerShellのバージョンや環境差で挙動が変わる点は注意。

---

## cmdとの違いが分かりにくいポイント

### `dir`

- **cmd**: 単なる文字列表示
- **PowerShell**: `Get-ChildItem` の結果として**オブジェクト**を返す

例:

```powershell
dir | where Length -gt 1MB
```

---

### `type` / `cat`

- **cmd の `type`** はテキストをそのまま表示
- **PowerShell の `type` / `cat`** は `Get-Content`

例:

```powershell
type .\memo.txt
cat .\memo.txt
gc .\memo.txt
```

全部ほぼ同じ意味です。

---

### `echo`

- **cmd**: 文字列表示の印象が強い
- **PowerShell**: `Write-Output` の別名

```powershell
echo 123
```

これは単なる表示だけでなく、**パイプに流せる出力**。

---

### `set`

- **cmd の `set`** は環境変数操作
- **PowerShell の `set`** は `Set-Variable`

つまり別物です。
PowerShellで環境変数を触るなら普通はこうします。

```powershell
$env:PATH
$env:TEMP = "C:\Temp"
```

---

### `cd`

- **cmd** と似ているが、PowerShellでは `Set-Location`
- レジストリや証明書ストアなど、**ファイルシステム以外にも移動できる**のが特徴

例:

```powershell
cd HKCU:
```

---

## よく使う実践セット

初心者がまず覚えるならこのあたりです。

| よく使う入力   | 実体            | 用途         |
| -------------- | --------------- | ------------ |
| `dir` / `ls`   | `Get-ChildItem` | 一覧表示     |
| `cd`           | `Set-Location`  | 移動         |
| `pwd`          | `Get-Location`  | 現在地確認   |
| `mkdir` / `md` | `New-Item`      | フォルダ作成 |
| `copy` / `cp`  | `Copy-Item`     | コピー       |
| `move` / `mv`  | `Move-Item`     | 移動         |
| `del` / `rm`   | `Remove-Item`   | 削除         |
| `cat` / `type` | `Get-Content`   | 内容表示     |
| `ps`           | `Get-Process`   | プロセス一覧 |
| `kill`         | `Stop-Process`  | 強制終了     |
| `cls`          | `Clear-Host`    | 画面クリア   |
| `help`         | `Get-Help`      | ヘルプ       |

---

## エイリアス確認コマンド

PowerShell上で実際に確認するには:

```powershell
Get-Alias
```

特定のエイリアスだけ見る:

```powershell
Get-Alias dir
Get-Alias ls
Get-Alias cat
```

逆に、あるコマンドにどんなエイリアスがあるか見る:

```powershell
Get-Alias | Where-Object Definition -eq Get-ChildItem
```

---

## cmdユーザー向けの覚え方

cmdからPowerShellへ移るなら、まずはこう覚えると楽です。

- `dir` → そのまま使える
- `cd` → そのまま使える
- `cls` → そのまま使える
- `copy`, `move`, `del` → だいたい使える
- ただし中身は **cmd命令ではなくPowerShellコマンドに置き換わっている**
- 真価は `| where`, `| select`, `| sort` のように**オブジェクト処理**できる点

---

## 実用例

### 1MB超のファイルだけ表示

```powershell
dir | where Length -gt 1MB
```

### txtファイルだけ表示

```powershell
dir *.txt
```

### ファイル内容から "error" を検索

```powershell
cat .\app.log | Select-String "error"
```

### メモ帳を終了

```powershell
ps notepad | kill
```
