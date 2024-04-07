# form_with
railsがセキュリティを考慮したうえでHTMLのformを作ってくれる。

### email_field

メールアドレスに＠を挿入してください。

### password_field

入力中文字が見えないようにしてくれる。

## モデルと紐づくform_with

```ruby
<h1>New User</h1>

<%= form_with model: @user do |f| %>
  <div class="mb-3">
    <%= f.label :email, class: 'form-label' %>
    <%= f.email_field :email, class: 'form-control' %>
  </div>
  <div class="mb-3">
    <%= f.label :password, class: 'form-label' %>
    <%= f.password_field :password, class: 'form-control' %>
  </div>
  <%= f.submit nil, class: 'btn btn-primary' %>
<% end %>

<div class="mt-3"><%= link_to 'Login?', login_path %></div>
```

@userを渡している。createアクションで`@user = User.new(user_params)`と定義しているので、受け取ったemailが格納され、エラーでrenderしても入力していたemailがフォームに入ったままになる。

### 実際の要素

```html
<div class="mb-3">
<label class="form-label" for="user_email">Email</label>
<input class="form-control" type="email" name="user[email]" id="user_email">
</div>
```

### type属性

email_fieldを指定しているので、type属性がemailになる。

### name属性

パラメーターの受け取り方が、モデルに紐づいてるかどうかで変わる。

## モデルと紐づかないform_with

loginなどDBのないformの場合はモデルと紐づかないformを使う。

```ruby
<h1>Login</h1>

<%= form_with url: login_path do |f| %>
  <div class="mb-3">
    <%= f.label :email, class: 'form-label' %>
    <%= f.email_field :email, class: 'form-control' %>
  </div>
  <div class="mb-3">
    <%= f.label :password, class: 'form-label' %>
    <%= f.password_field :password, class: 'form-control' %>
  </div>
  <%= f.submit nil, class: 'btn btn-primary' %>
<% end %>

<div class="mt-3"><%= link_to 'Sign up?', new_user_path %></div>
```

インスタンスを渡してないので、リダイレクトで入力してた内容が消える。

### 実際の要素

```html
<div class="mb-3">
<label class="form-label" for="email">Email</label>
<input class="form-control" type="email" name="email" id="email">
</div>
```

### label

formにはlabel（ボックスの上の文字列）とinputを紐づける機能がある。labelのfor属性と同じ値が入っているinput属性と紐づく。

## paramsについて

```bash
#<ActionController::Parameters {"authenticity_token"=>"M7BylTQJO3IEa5DGiQPgMFNwMANtB3Ux2913bFok3IHLqOyDhr7uVAOnJGFfc0d1AoL4mA_oRXhJE2WjeEQP0w", "task"=>{"title"=>"Rails入門", "body"=>"test"}, "commit"=>"Create Task", "controller"=>"tasks", "action"=>"create"} permitted: false>
```

モデルに紐づいたformだとname属性がモデルで括られる。ストロングパラメータで受け取る値を指定して安全に受け取れる。ストロングパラメータを使わない方法だと、@task = Task.new(title: params[:title], body: params[:body])のように毎回書かないといけない。
