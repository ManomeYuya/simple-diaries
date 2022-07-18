# README

# アプリ名
simple-diaries

# アプリケーション概要


# URL

# テスト用アカウント
・Basic認証ID：
・Basic認証パスワード:
・メールアドレス：
・パスワード：
# 利用方法

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