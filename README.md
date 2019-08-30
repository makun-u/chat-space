# chat-space DB設計

## usersテーブル
|Column|Type|Options|
|:--------:|:--------:|:--------:|
|email|string|null: false|
|password|string|null: false|
|username|string|null: false|
### Association
- has_many :messages
  has_many :groups_users
- has_many :groups, through: :groups_users

### add_index
- add_index :users,  [:username, :email]
---

## messagesテーブル
|Column|Type|Options|
|:--------:|:--------:|:--------:|
|body|text|null: false|
|image|string||
|user_id|integer|null: false, foreign_key: true|
|group_id|integer|null: false, foreign_key: true|
### Association
- belongs_to :group
- belongs_to :user
---

## groupsテーブル
|Column|Type|Options|
|:--------:|:--------:|:--------:|
|groupname|string|null: false|
### Association
- has_many :messages
- has_many :groups_users
- has_many :users, through: :groups_users

### add_index
- add_index :groups, :groupname
---

## groups_usersテーブル
|Column|Type|Options|
|:--------:|:--------:|:--------:|
|group_id|integer|null: false, foreign_key: true|
|user_id|integer|null: false, foreign_key: true|
### Association
- belongs_to :group
- belongs_to :user