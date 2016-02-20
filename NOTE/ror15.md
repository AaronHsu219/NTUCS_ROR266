## Association (關聯)
* 假設今天我們要建立一個類似 Netflix 的服務，叫 Youflix  
* 參考 Netflix 的介面，觀察需要的資料表
* 我們需要的資料表：
    * Video: 用來記錄所有的影片訊息
    * Category: 用來記錄所有的影片類別
    * User: 用來記錄所有的使用者訊息
    * User 與 Video 是一對多關係
    * Category 與 Video 是多對多關係
* 建立 videos 資料表：
```
rails g migration add_videos_table
```
```ruby
class AddVideosTable < ActiveRecord::Migration
  def change
    create_table :videos do |t|
      t.string :title
      t.text   :description

      t.timestamp
    end
  end
end
```    
* 建立 Categories 資料表：
```
    rails g migration add_categories_table
```
```ruby
    class AddCategoriesTable < ActiveRecord::Migration
    def change
        create_table :categories do |t|
        t.string :title
        end

        create_table :connections do |t|
        t.integer :video_id
        t.integer :category_id
        end
    end
    end
```

* 設定 Model 檔案：
```ruby
    class Video < ActiveRecord::Base
    has_many :connections
    has_many :categories, through: :connections
    end

    #我們的 join table
    class Connection < ActiveRecord::Base
    belongs_to :video
    belongs_to :category
    end

    class Category < ActiveRecord::Base
    has_many :connections
    has_many :videos, through: :connections
    end
```

* 測試我們建立的關聯是否成功：
```ruby
    # 開啟 rails console:

    ironman = Video.create(title: "Iron Man", description: "I am Iron man")

    cat1 = Category.create(title: "Action")

    cat2 = Category.create(title: "Hollywood")

    # 搜尋 Iron man 這部電影所有的 categories

    ironman.categories 

    # 目前是一個空陣列，現在我們把兩個 category 綁定到 Iron man 

    ironman.categories << cat1

    ironman.categories << cat2

    # 再查一次，就會發現 ironman 已經和兩個 category 綁定了

    ironman.categories
```

* 測試我們建立的關聯是否成功：
```ruby           
    # 當然 association 是雙向性的，所以我也應該要能透過 category 搜尋到 video
    cat1.videos
``` 

* 建立 users 資料表：
```ruby
    class AddUsersTable < ActiveRecord::Migration
    def change
        create_table :users do |t|
        t.string :name
        t.string :email
        end

        #要為 user 和 video 建立一對多關係，多的一方需要欄位紀錄少的一方的 id
        #命名就用 少的一方的 model 名加上 "_id"
        add_column :videos, :user_id, :integer
    end
    end
```

* 設定 Model 檔案：
```ruby
    class Video < ActiveRecord::Base
    belongs_to :user

    has_many :connections
    has_many :categories, through: :connections
    end

    class User < ActiveRecord::Base
    has_many :videos
    end
```

* 測試我們建立的關聯是否成功：
```ruby
    # 創造一個使用者

    user = User.create(name: "Bob", email: "bob@gmail.com")

    # 搜尋這個使用者的 videos

    user.videos

    #沒有任何東西 

    找出我們之前建立的兩個 video

    video1 = Video.find(1)
    video2 = Video.find(2)

    user.videos << video1
    user.videos << video2


    # 再搜尋一次這個使用者的 videos

    user.videos
```

##　find vs where vs find_by　　
```ruby
    # find 是透過資料的 id 搜尋

    user = User.find(1) #尋找 users 資料表裡 id 為 1 的 record

    # where 是透過給訂的條件搜尋

    result = User.where(name: "bob") # 會回傳一個有一或多筆 user 的陣列

    # ActiveRecord 會有內建的搜尋方法，find_by_

    bob = User.find_by_name("bob")

    # 問題是，find_by_ 只會回傳符合條件的第一筆資料，請小心使用
```

##　Validation (驗證)
```ruby
    # 我們要確保資料輸入的正確性
    # 像是 User 要是沒有 name 和 email，就不該被建立

    class User < ActiveRecord::Base
    validates :name, presence: true
    validates :email, presence: true
    end
```

```ruby
    # 我們要確保輸入的名字有一定的長度

    class User < ActiveRecord::Base
    validates :name, presence: true
    validates :name, length: { minimum: 2 }
    validates :name, length: { maximum: 200 }
    #名字最少要有兩個英文字母，最多不可超過兩百個英文字母
    
    validates :email, presence: true

    end
```

```ruby
    # 我們要確保輸入的名字有一定的長度

    class User < ActiveRecord::Base
    validates :name, presence: true
    validates :name, length: { minimum: 2 }
    validates :name, length: { maximum: 200 }
    
    validates :email, presence: true
    validates :email, uniqueness: true
    #任何 email 應該都是獨一無二的，所以應該卻確保它的獨特性

    end
```

```ruby
    # 我們要確保輸入的名字有一定的長度

    class User < ActiveRecord::Base
    validates :name, presence: true
    validates :name, length: { minimum: 2 }
    validates :name, length: { maximum: 200 }
    
    validates :email, presence: true
    validates :email, uniqueness: true
    #任何 email 應該都是獨一無二的，所以應該卻確保它的獨特性

    end
```
* 更多驗證  
    http://rails.ruby.tw/active_record_validations.html