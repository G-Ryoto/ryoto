# furimaアプリ

# アプリ名
フリマアプリ

# アプリケーションの概要
ユーザーを登録すると商品を出品できるようになります。自身が出品した商品は、編集と削除をすることができます。
他のユーザーが出品した商品は、クレジットカードを持ちて購入することができます。

# URL
Renderによるデプロイ
https://furima-38957.onrender.com

Basic認証
・ID：admin
・PASS：2222

# テスト用アカウント

購入者
・メールアドレス：　sakura@gmail.com
・パスワード：Sakura2023

購入者カード情報（PAYJPテスト用）
・番号：4242424242424242
・期限：７月/（20）2３年（未来の年月であれば可能）
・セキュリティコード：123

出品者用
・メールアドレス名：momiji@gmail.com
・パスワード：Momiji2023

# README　テーブル設計

## usersテーブル
| Column            |  Type  |  Options   |
| ----------------- | ------ | ---------- |
| first_name        | string | null:false |
| family_name       | string | null:false |
| family_name_kana  | string | null:false |
| first_name_kana   | string | null:false |
| email             | string | null:false,unique: true |
| nickname          | string | null:false |
| encrypted_password | string | null:false |
| birth_day         | date   | null:false |

### Association
has_many :products 
has_many :orders

## paymentsテーブル
| Column            |  Type  |  Options   |
| ----------------- | ------ | ---------- |
| post_code         | string | null:false | 
| prefecture_id     | integer | null:false | 
| city              | string | null:false | 
| address           | string | null:false |
| building_name     | string |            |
| phone_number      | string | null:false |
| wallet            | references | foreign_key: true | 

### Association
belongs_to :wallet 

## ordersテーブル
| Column            |  Type  |  Options   |
| ----------------- | ------ | ---------- |
| user              | references | null: false, foreign_key: true |
| product           | references | null: false, foreign_key: true |

### Association
belongs_to :user
belongs_to :product
has_one :destination

## itemsテーブル
| Column            | Type   |  Options   |
| ----------------- | ------ | ---------- |
| name              | string | null:false |
| user              | references | null: false, foreign_key: true |
| price             | integer | null:false |
| description       | text   | null:false | 
| status_id         | integer | null:false |
| category_id       | integer | null:false |
| shipping_charge_id | integer | null:false | 
| shipping_day_id  | integer | null:false |  
| prefecture_id     | integer | null:false | 

### Association
belongs_to :user
has_one :order
