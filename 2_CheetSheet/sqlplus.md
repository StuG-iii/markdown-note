# SQL*Plus チートシート

- [SQL\*Plus チートシート](#sqlplus-チートシート)
  - [1. 起動・接続](#1-起動接続)
  - [2. 基本的なSQL実行](#2-基本的なsql実行)
  - [3. SQLファイル実行](#3-sqlファイル実行)
  - [4. 出力表示の整形](#4-出力表示の整形)
  - [5. 件数・経過時間・実行内容の表示](#5-件数経過時間実行内容の表示)
  - [6. スプール出力](#6-スプール出力)
  - [7. 変数](#7-変数)
    - [置換変数](#置換変数)
    - [バインド変数](#バインド変数)
  - [8. PL/SQL実行](#8-plsql実行)
  - [9. テーブル・オブジェクト確認](#9-テーブルオブジェクト確認)
  - [10. 現在のユーザーや接続先確認](#10-現在のユーザーや接続先確認)
  - [11. SQL\*Plus環境確認](#11-sqlplus環境確認)
  - [12. よく使うSETコマンド](#12-よく使うsetコマンド)
  - [13. 検索・編集補助](#13-検索編集補助)
  - [14. よくある実務用テンプレート](#14-よくある実務用テンプレート)
    - [見やすく検索](#見やすく検索)
    - [DBMS\_OUTPUT確認](#dbms_output確認)
    - [結果をファイル保存](#結果をファイル保存)
    - [スクリプト実行時の定番](#スクリプト実行時の定番)
  - [15. 覚えておくと便利なコマンド](#15-覚えておくと便利なコマンド)
  - [16. 最低限これだけ覚える版](#16-最低限これだけ覚える版)

## 1. 起動・接続

```bash
sqlplus username/password@hostname:1521/servicename
```

```bash
sqlplus username/password
```

OS認証:

```bash
sqlplus / as sysdba
```

接続し直し:

```sql
CONNECT username/password
CONNECT / AS SYSDBA
```

切断・終了:

```sql
DISCONNECT
EXIT
QUIT
```

---

## 2. 基本的なSQL実行

```sql
SELECT * FROM employees;
```

```sql
INSERT INTO test_table (id, name) VALUES (1, 'Alice');
UPDATE test_table SET name = 'Bob' WHERE id = 1;
DELETE FROM test_table WHERE id = 1;
```

確定・取消:

```sql
COMMIT;
ROLLBACK;
```

---

## 3. SQLファイル実行

スクリプト実行:

```sql
@script.sql
START script.sql
```

引数付き:

```sql
@script.sql value1 value2
```

`script.sql` 内で引数参照:

```sql
SELECT '&1', '&2' FROM dual;
```

---

## 4. 出力表示の整形

行幅設定:

```sql
SET LINESIZE 200
```

1ページの行数:

```sql
SET PAGESIZE 100
```

長い列の折り返し制御:

```sql
SET WRAP OFF
```

NULL表示:

```sql
SET NULL '(null)'
```

列見出し設定:

```sql
COLUMN employee_name HEADING 'Employee Name'
```

列幅設定:

```sql
COLUMN employee_name FORMAT A20
COLUMN salary FORMAT 999,999
```

実行結果確認しやすくする定番:

```sql
SET LINESIZE 200
SET PAGESIZE 100
SET TRIMSPOOL ON
SET TAB OFF
```

---

## 5. 件数・経過時間・実行内容の表示

SQL実行を画面に出す:

```sql
SET ECHO ON
```

実行したSQLを表示:

```sql
LIST
```

実行計画や統計向け補助:

```sql
SET TIMING ON
SET AUTOTRACE ON
SET AUTOTRACE TRACEONLY
```

※ `AUTOTRACE` は環境によって使えない場合があります。

---

## 6. スプール出力

画面出力をファイル保存:

```sql
SPOOL output.txt
SELECT * FROM employees;
SPOOL OFF
```

追記:

```sql
SPOOL output.txt APPEND
```

HTML形式風にしたい場合:

```sql
SET MARKUP HTML ON
SPOOL report.html
SELECT * FROM employees;
SPOOL OFF
SET MARKUP HTML OFF
```

---

## 7. 変数

### 置換変数

入力を促す:

```sql
SELECT * FROM employees WHERE department_id = &dept_id;
```

毎回聞かれたくない場合:

```sql
DEFINE dept_id = 10
SELECT * FROM employees WHERE department_id = &dept_id;
```

確認:

```sql
DEFINE
```

解除:

```sql
UNDEFINE dept_id
```

### バインド変数

作成:

```sql
VARIABLE v_name VARCHAR2(50)
```

代入:

```sql
BEGIN
  :v_name := 'Alice';
END;
/
```

表示:

```sql
PRINT v_name
```

---

## 8. PL/SQL実行

PL/SQLブロック:

```sql
BEGIN
  DBMS_OUTPUT.PUT_LINE('Hello');
END;
/
```

`DBMS_OUTPUT` を表示する:

```sql
SET SERVEROUTPUT ON
```

サイズ指定:

```sql
SET SERVEROUTPUT ON SIZE 1000000
```

---

## 9. テーブル・オブジェクト確認

テーブル一覧:

```sql
SELECT table_name FROM user_tables;
SELECT table_name FROM all_tables;
SELECT table_name FROM dba_tables;
```

構造確認:

```sql
DESC employees
DESCRIBE employees
```

インデックス一覧:

```sql
SELECT index_name, table_name FROM user_indexes;
```

シーケンス一覧:

```sql
SELECT sequence_name FROM user_sequences;
```

ビュー一覧:

```sql
SELECT view_name FROM user_views;
```

---

## 10. 現在のユーザーや接続先確認

現在のユーザー:

```sql
SHOW USER
```

接続情報確認:

```sql
SELECT sys_context('USERENV', 'SESSION_USER') FROM dual;
SELECT sys_context('USERENV', 'DB_NAME') FROM dual;
SELECT sys_context('USERENV', 'SERVICE_NAME') FROM dual;
SELECT sys_context('USERENV', 'HOST') FROM dual;
```

---

## 11. SQL*Plus環境確認

設定確認:

```sql
SHOW ALL
```

特定設定確認:

```sql
SHOW PAGESIZE
SHOW LINESIZE
SHOW SERVEROUTPUT
```

---

## 12. よく使うSETコマンド

```sql
SET ECHO ON
SET FEEDBACK ON
SET HEADING ON
SET VERIFY OFF
SET PAGESIZE 100
SET LINESIZE 200
SET SERVEROUTPUT ON
SET TIMING ON
SET TERMOUT ON
SET TRIMSPOOL ON
```

意味の要点:

- `ECHO ON` : スクリプト中のSQLも表示
- `FEEDBACK ON` : “14 rows selected” など表示
- `HEADING ON` : 列名表示
- `VERIFY OFF` : 置換前後の表示を抑制
- `TERMOUT OFF` : スクリプト実行時の画面出力を抑制
- `SERVEROUTPUT ON` : `DBMS_OUTPUT.PUT_LINE` を表示

---

## 13. 検索・編集補助

バッファ中SQLの確認:

```sql
LIST
```

再実行:

```sql
/
RUN
```

1行修正:

```sql
CHANGE /old/new
```

バッファクリア:

```sql
CLEAR BUFFER
```

---

## 14. よくある実務用テンプレート

### 見やすく検索

```sql
SET LINESIZE 200
SET PAGESIZE 100
COLUMN username FORMAT A20
COLUMN account_status FORMAT A20

SELECT username, account_status
FROM dba_users
ORDER BY username;
```

### DBMS_OUTPUT確認

```sql
SET SERVEROUTPUT ON

BEGIN
  DBMS_OUTPUT.PUT_LINE('test');
END;
/
```

### 結果をファイル保存

```sql
SET PAGESIZE 100
SET LINESIZE 200
SET TRIMSPOOL ON
SPOOL result.txt

SELECT * FROM employees;

SPOOL OFF
```

### スクリプト実行時の定番

```sql
SET ECHO ON
SET VERIFY OFF
SET FEEDBACK ON
SET SERVEROUTPUT ON
```

---

## 15. 覚えておくと便利なコマンド

```sql
HELP
HOST
! ls
```

- `HELP` : ヘルプ
- `HOST` : OSコマンド実行
- `!` : 環境によってはOSコマンド実行

例:

```sql
HOST dir
HOST ls
```

---

## 16. 最低限これだけ覚える版

```sql
CONNECT user/password
SELECT * FROM table_name;
DESC table_name
SET LINESIZE 200
SET PAGESIZE 100
SET SERVEROUTPUT ON
SPOOL output.txt
@script.sql
COMMIT;
ROLLBACK;
EXIT
```