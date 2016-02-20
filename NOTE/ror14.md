# 手動打造一個 Action
1. 產生＆編輯 migration 檔案
2. 執行 rake db:migrate 改變資料庫
3. 建立和該 table 相對應的 model 檔
3. 寫出 Controller 檔案，宣告 action
4. 在 routes.rb 裡設定路由
5. 產生 view 所需要的 html.erb 檔案

## (1) 產生 Migration (資料遷移) 檔案
```
$rails g migration add_users_table
```
產生 Migration (資料遷移) 檔案  
migration 檔不必用 SQL 語法，直接用 ruby 語法即可在資料庫裡修改 schema  
```ruby
class AddUsersTable < ActiveRecord::Migration
  def change
    create_table :users do |t|
      t.string :name
      t.string :phone
      t.integer :age

      t.timestamps null: false
    end
  end
end
```

## (2) 執行 rake db:migrate
```ruby
$rake db:migrate
```
寫完 migration 檔之後，需要執行 rake db:migrate，實際的 database 才會發生變動

## (3) 建立和該 table 相對應的 model 檔  
```ruby
# 在 app/models 底下建立一個新的檔案，記得命名要單數
class User < ActiveRecord::Base

end
```

## (4) 寫出 Controller 檔案，宣告 action  
```ruby
# 在 app/controller 底下建立一個新的檔案，記得命名是 model 名字、複數加上 controller
class UsersController < ApplicationController
  def index
  end
end
```

## (5) 在 routes.rb 裡設定路由
```ruby
Rails.application.routes.draw do
  # 宣告單一路徑
  get 'users' => 'users#index'

  # 或是用 resources 宣告整組路徑
  resources :users

end
```

## (6) 產生 view 所需要的 html.erb 檔案
```ruby
# 在 app/views/ 底下建立一個新的資料夾，命名是 model 的複數
# 然後再建立和 action 名字相同的 html.erb 檔

<h1>Hello World!</h1>

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Phone</th>
      <th>Age</th>
      <th colspan="3"></th>
    </tr>
  </thead>

  <tbody>
    <%= @users.each do |user| %>
      <tr>
        <td><%= user.name %></td>
        <td><%= user.phone %></td>
        <td><%= user.age %></td>
      </tr>
    <% end %>
  </tbody>
</table>
```

# MVC 就從 M 開始
資料庫是網路應用的基礎  
打造好的動態網頁就要從設計完善的DB開始

## DB Schema
資料庫的藍圖  
紀錄每個資料表的欄位名稱  
紀錄每個資料表與其他資料表的關聯性  
所以我們剛才實作的 migration 檔  
其實就是在紀錄 schema 的改變  

## ActiveRecord
每一個 migration 檔都是一個繼承於 Active Record 的 class  
```ruby
class CreateOrders < ActiveRecord::Migration
```
Active Record 是 Rails 應用程式中的 Models 基礎。  
它提供了 CRUD 功能、先進的查詢能力以及可以跟其他 Models 關聯的功能。

## CRUD
任何資料結構或型別最基礎的四種操作方式： 
CREATE - 新增資料  
READ - 讀取資料  
UPDATE - 編輯資料  
DELETE - 刪除資料

## ActiveRecord
每一個 model 檔也是繼承於 Active Record 的 class
```ruby
class Order < ActiveRecord::Base
end
```
一個 model 檔是對映到一個資料庫裡的資料表

## Association (關聯)
* 資料表之間的關係要如何設定?  

```ruby
  class User < ActiveRecord::Base
    has_many :orders
  end

  class Order < ActiveRecord::Base
    belongs_to :user
  end
```
* 常見的 association
```ruby
  # 一對一
  # 一對多

  belongs_to
  has_one
  has_many

  # 多對多

  has_many :through
  has_and_belongs_to_many :user
```

## Rails Console
測試 Active Record 的設定是否有正常運作  
```ruby
$rails console
或
$rails c
```
具備 irb 功能 ，不過是專屬於一個 rails project

## 官方文件
Association 官方文件  
http://rails.ruby.tw/association_basics.html
 
Migration 官方文件  
http://rails.ruby.tw/active_record_migrations.html

Active Record 官方文件  
http://rails.ruby.tw/active_record_basics.html


## 功課
打造留言板所需要的 database  
寫好 migration 檔  
建立 routing 和 model 檔  

留言板 demo:  
https://postit-eugene-chang.herokuapp.com/  
