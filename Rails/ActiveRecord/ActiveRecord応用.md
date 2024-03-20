## 範囲オブジェクト(Range)
Railsのwhereメソッドでは範囲オブジェクト(Range)を使うことができる。
### x以下
idが10以下のユーザー
```ruby
User.where(id: ..10)
```
発行されるSQL
```sql
SELECT "users".* FROM "users" WHERE "users"."id" <= $1  [["id", 10]]
```
### x未満
idが１０未満のユーザー
```ruby
User.where(id: ...10)
```
発行されるSQL
```sql
SELECT "users".* FROM "users" WHERE "users"."id" < $1  [["id", 10]]
```
### x以上
idが１０以上のユーザー
```ruby
User.where(id: 10..)
```
発行されるSQL
```sql
SELECT "users".* FROM "users" WHERE "users"."id" >= $1  [["id", 10]]
```
### xより大きい
「より大きい」の場合は次のように書く必要がある。
```ruby
User.where('id > ?', 10)
```
```sql
SELECT "users".* FROM "users" WHERE "users"."id" > $1  [["id", 10]]
```
