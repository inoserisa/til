## Active Recordとは
ActiveRecordはRailsのデフォルトのORM(Object-Relational Mapping)ライブラリであり、Railsのモデル層の実装に使用される。ORMは、データベースとのやりとりを簡単にするツール。

### メソッド
#### Create(生成)に関するメソッド
```ruby
@blog = Blog.new(title: "タイトル", content: "内容")
#blogモデルのインスタンスを作成

@blog = Blog.build(title: "タイトル", content: "内容")
#newと同じ、可読性を上げるため関連モデルのインスタンスにするときによく使われる

@blog.save
#newやbuildで作った@blogをDBに保存する

Blog.create(title: "タイトル", content: "内容")
#newとsaveを組み合わせて生成と同時にDBへ保存する
```
#### Read(参照)に関するメソッド
```ruby
@blog = Blog.all
#blogsテーブルから全レコードを配列として取得

@blog = Blog.first
#blogsテーブルのidが一番小さいレコードを取得

@blog = Blog.last
#blogsテーブルのidが一番大きいレコードを取得

@blog = Blog.find(1)
#引数に入っている数字と同じidのレコードを取得

@blog = Blog.find_by(title: "タイトル")
#引数に入っている条件と合っているもので一番若いidのレコードを取得

@blog = Blog.where(title: "タイトル")
#引数に入っている条件と合っているすべてのレコードを取得

@blog = Blog.order(id: :desc)
#引数に入っているカラムを:asc(昇順)または:desc(降順)に並び替えてレコードを取得

@blog = Blog.select(:title)
#引数に入っている名前のカラムのみを取得

@blog = Blog.limit(3)
#引数に入っている数字の数だけidの若い順にレコードを取得
```
#### Update(更新)に関するメソッド
```ruby
@blog.update
#findやfind_byで取得したレコードを元に更新
```
#### Delete(削除)に関するメソッド
```ruby
@blog.destroy
#findやfind_byで取得したレコードを削除
```
