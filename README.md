# README

# アプリ名
one-line-diary

# アプリケーション概要


# URL

# テスト用アカウント
・Basic認証ID：admin
・Basic認証パスワード：2222
・メールアドレス：test@com
・パスワード：test11
# 利用方法

## 日記を投稿する
・
・
・

## 
・
・

## 
・

# アプリケーションを作成した背景


# 洗い出した要件
要件定義シート
https://docs.google.com/spreadsheets/d/1uyNWhry767kxWGf87YFPNGWLwunnpXS5vRqNqAVHG2M/edit#gid=982722306

# 追加実装したい機能
・管理者制限：不適切な投稿を削除したりユーザーを制限することでサービスの安全性を高めるため
・

# データベース設計

## users テーブル

|Column            |Type   |Options    |
|------------------|-------|-----------|
|name              |string|null: false|
|email             |string|null: false, unique: true| 
|encrypted_password|string|null: false|


### Association

 - has_many :diaries
 - has_many :comments
 - has_many :likes

 ## comments テーブル

| Column   | Type      | Options     |
| ---------| --------- | ----------- |
| user_id  | integer   |null: false, foreign_key: true|
| diary_id | integer   |null: false, foreign_key: true|
| text     | text | null: false|

### Association

 - belongs_to :user
 - belongs_to :diary

 ## likes テーブル

| Column   | Type      | Options     |
| ---------| --------- | ----------- |
| user_id  | integer   |null: false, foreign_key: true|
| diary_id | integer   |null: false, foreign_key: true|

### Association

 - belongs_to :user
 - belongs_to :diary


## tags テーブル

| Column   | Type      | Options     |
| ---------| --------- | ----------- |
| tag_name | string    |null: false|

### Association

 - belongs_to :user
 - has_many :diaries, through: :diary_tags
 - has_many :diary_tags

 ## diaries テーブル

| Column   | Type      | Options     |
| ---------| --------- | ----------- |
| text     | text   |null: false|
| user_id  | references|null: false, foreign_key: true|

### Association

 - belongs_to :user
 - has_many :tags, through: :diary_tags
 - has_many :diary_tags
 - has_many :likes
 - has_many :comments

 ## diary_tags テーブル

| Column   | Type      | Options     |
| ---------| --------- | ----------- |
| tag_name_id  |integer|null: false, foreign_key: true|
| diary_id  |integer|null: false, foreign_key: true|

### Association

 - belongs_to :diary
 - belongs_to :tag