#!/bin/bash

# 必須の変数
BUCKET_NAME="your-s3-bucket-name"  # S3バケット名
FILE_PATH="./local_file.txt"      # アップロードするファイルパス
S3_PATH="path/in/s3/"             # S3バケット内のパス

# AWS CLIでファイルをアップロード
aws s3 cp "$FILE_PATH" "s3://$BUCKET_NAME/$S3_PATH"

# アップロード結果の確認
if [ $? -eq 0 ]; then
  echo "アップロード成功: $FILE_PATH -> s3://$BUCKET_NAME/$S3_PATH"
else
  echo "アップロード失敗"
fi


PostgreSQLでもストアドプロシージャ（stored procedures）をサポートしていますが、他のRDBMS（例：OracleやSQL Server）と少し異なる点があります。以下に、PostgreSQLでのストアドプロシージャ対応について概要を説明します。

---

PostgreSQLでもストアドプロシージャ（stored procedures）をサポートしていますが、他のRDBMS（例：OracleやSQL Server）と少し異なる点があります。以下に、PostgreSQLでのストアドプロシージャ対応について概要を説明します。

---

### ✅ PostgreSQLのストアドプロシージャ概要

PostgreSQL 11以降では、`CREATE PROCEDURE`構文が導入され、**トランザクション制御が可能なストアドプロシージャ**が正式にサポートされました。

#### 1. **CREATE PROCEDURE構文**
```sql
CREATE PROCEDURE sample_procedure(IN param1 INT, OUT result TEXT)
LANGUAGE plpgsql
AS $$
BEGIN
    -- 処理内容
    result := '処理完了: ' || param1;
END;
$$;
```

#### 2. **CALL文による実行**
```sql
CALL sample_procedure(100, result);
```

#### 3. **トランザクション制御**
ストアドプロシージャ内で `BEGIN`, `COMMIT`, `ROLLBACK` を使用可能です。これは `CREATE FUNCTION` ではできません。

---

### ✅ PostgreSQLの関数（CREATE FUNCTION）との違い

| 項目 | CREATE FUNCTION | CREATE PROCEDURE |
|------|------------------|------------------|
| トランザクション制御 | ❌ 不可 | ✅ 可能 |
| 戻り値 | ✅ あり | ❌ なし（OUTパラメータで返す） |
| 呼び出し方法 | `SELECT`や`PERFORM` | `CALL` |

---

### ✅ よく使われる用途

- バッチ処理
- 複雑な業務ロジックのカプセル化
- 複数ステップのトランザクション処理

---

### ✅ 注意点

- ストアドプロシージャは `CALL` でしか呼び出せません。
- `RAISE NOTICE` などでログ出力可能。
- `LANGUAGE plpgsql` が一般的ですが、SQLや他言語も使用可能。

---

もし、既存のOracleやSQL ServerのストアドプロシージャをPostgreSQLに移植したい場合は、構文の違いやトランザクション制御の扱いに注意が必要です。具体的なコード例や移植のサポートもできますので、必要であれば教えてください。

何か特定のストアドプロシージャをPostgreSQLに対応させたいですか？それとも基本的なテンプレートが欲しいですか？

---

もし、既存のOracleやSQL ServerのストアドプロシージャをPostgreSQLに移植したい場合は、構文の違いやトランザクション制御の扱いに注意が必要です。具体的なコード例や移植のサポートもできますので、必要であれば教えてください。

何か特定のストアドプロシージャをPostgreSQLに対応させたいですか？それとも基本的なテンプレートが欲しいですか？
