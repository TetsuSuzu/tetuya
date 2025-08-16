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
