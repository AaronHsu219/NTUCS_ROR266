## HTML & CSS
https://www.codecademy.com/learn/web  
http://www.w3schools.com/  
http://www.w3school.com.cn/  ​

## 推薦的書：
http://duck-on-rails.herokuapp.com/posts/eloquent-ruby  

## Unless
```ruby
# 文法上可以想成 "除非"

var = false

# 寫在符合條件要執行的程式碼後方
puts "It's true" unless var
```

## Conditional Assignment
```ruby
favorite_book = nil
puts favorite_book

#如果 favorite book 還沒有被設值，那就把它設定成左邊的值
favorite_book ||= "麥田捕手"
puts favorite_book

# => 麥田捕手

# 若變數已經有值，就不會設定新的值給它
favorite_book ||= "1984"
puts favorite_book

# => 麥田捕手
```

## Implicit Return
```ruby
# 在 ruby 的 method 裡，其實在大部份的情況下不需要 return 關鍵字

def greater_than_five(operation)
  if operation >= 5
    true
  else
    false
  end
end

operation = 5 
puts greater_than_five(operation)
#印出 true

def area_of_circle(radius)
  radius_squared = radius ** 2
  area = radius_squared * 3.14
  # 重點是，ruby 會回傳最後一行被計算的結果
end

puts area_of_circle(10)
# 印出 314.0
```

## Object Oriented物件導向
物件導向  
程式設計的思維  
封裝資料和方法到物件裡  
封裝後的程式碼可被重複使用  

Ruby 語言裡，任何東西都是物件  

##　Class (類別)
```ruby
# 可以想像成樣板
# 宣告一個叫 Person 的 class
# 注意 class 名稱要用 CamelCase，也就是每一個字的第一字母要大寫
class Person
  # 任何 class 一定要加建構式
  def initialize(name) # 建構式
    @name = name # 物件變數
  end

  def greet_me(word)
    puts "#{word}, #{@name}"
  end

end

# 用 new 創出兩個 person 的物件
eugene = Person.new("Eugene")
overlord = Person.new("Overlord88")

# person 物件才能使用 greet_me() 方法
eugene.greet_me("Good Morning")
#印出 Good Morning, Eugene
overlord.greet_me("Hello")
#印出 Hello, Overlord88
```

## initialize
```ruby
class Person
  # 每一個 person 物件在創出時會被呼叫到
  # 正式名稱是 constructor (建構式)
  def initialize
    puts "This object was initialized!"
  end
end

bob = Person.new     
# => "This object was initialized!"
```

## Accessor Method
```ruby
# 假設我只想印出 bob 的歲數，我需要讀取 @name
class Person
  def initialize(name, age)
    @name = name
    @age = age
  end

  def greet
    puts "Hello, my name is #{@name}"
  end
end

bob = Person.new("bob", 17)
bob.name
# => accessor_method.rb:14:in `<main>': 
#undefined method `name' for #<Person:0x007facfa838188 @name="bob", @age=17> (NoMethodError)
```

```ruby
# 為了取值，必須要寫一個 method 叫物件回傳 @name

class Person
  def initialize(name, age)
    @name = name
    @age = age
  end

  def greet
    puts "Hello, my name is #{@name}"
  end
  # 定義 get_name
  def get_name
    @name
  end
end

bob = Person.new("bob", 17)
puts bob.get_name
# => bo
```

```ruby
# 假設我是要寫入或更改 @name
# 不能直接使用 bob.name = "Bob"
class Person
  def initialize(name, age)
    @name = name
    @age = age
  end

  def greet
    puts "Hello, my name is #{@name}"
  end
  # 讀取資料方法，稱為 getter method
  def get_name
    @name
  end
  # 寫入/更改方法，稱為 setter method
  def set_name=(name)
    @name = name
  end
end

bob = Person.new("bob", 17)
bob.set_name = "Bob"
puts bob.get_name
# => Bob
```

```ruby
# 當然每次寫 getter 和 setter method 很麻煩，所以聰明的 ruby 就有了 attr_accessor 方法
class Person
  # 在 attr_accessor 關鍵字後方加上 instance method 的 symbol
  # 自動幫使用者把 getter 和 setter method 寫好
  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end

  def greet
    puts "Hello, my name is #{@name}"
  end
end

bob = Person.new("bob", 17)
bob.name = "Bob"
bob.age = 30
puts bob.name
puts bob.age
# => Bob
# => 30
```

## Instance Variable
```ruby
# instance variable(實例變數) 是把資料綁定在 object 上的方法
# 只要被創出來的 object 還存在，instance variable 紀錄的資料也存在

class Person
  def initialize(name, age)
    # instance variable 前面一定要加 @
    @name = name
    @age = age
  end
end
```

```ruby
# instance method(實例方法) 是只有被創造出來的物件才可使用
class Person
  def initialize(name, age)
    # instance variable 等同於在這個 class 的區域變數
    @name = name
    @age = age
  end

  # 宣告 instance methods，就像宣告一般的 method，只不過在 class 裡面
  def greet
    # instance variable 只可在 class 裡面被使用
    puts "Hello, my name is #{@name}"
  end
end

bob = Person.new("bob", 17)
bob.greet
# => Hello, my name is bob

# 若沒有先創出 Person 的instance (實例)，也就是先 new 一個 Person 的 object
# 使用 instance method 就會噴錯
Person.greet
# => instance_method.rb:22:in `<main>': 
# undefined method `greet' for Person:Class (NoMethodError)
```

##　Self
```ruby
# 現在我們知道用 attr_accessor，Ruby 會自動把 getter 
# 和 setter method 產生出來
class Person
  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end

  def greet
    puts "Hello, my name is #{name}"
  end
  # 但假設說我需要在 class 裡面其他的 instance method 裡
  # 呼叫 getter 和 setter method
  def change_info(n, a)
    # 希望能像在使用 setter method 一樣， bob.name = "Boob"
    name = n
    age = a
  end
end

bob = Person.new("bob", 17)
bob.change_info("Bob", 30)

puts bob.name
# => bob
puts bob.age
# => 17
# 但是 bob 的資料卻沒變，為什麼？ 
# ruby 以為我們在 change_info 裡的 name 和 age 是指變數而不是 getter method
```

```ruby
class Person
  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end

  def greet
    puts "Hello, my name is #{self.name}"
  end
  # 為了確保 ruby 知道我們是要使用 Person 的 getter 和 setter method
  # 需要 self 這個關鍵字
  def change_info(n, a)
    self.name = n
    self.age = a
  end

  def print_info(name, age)
    self.change_info(name, age)
    puts self.name 
    puts self.age
  end
end

bob = Person.new("bob", 17)
bob.change_info("Bob", 30)
puts bob.name
# => Bob
puts bob.age
# => 30
```

```ruby
# self 可用於：
# 1. 在 class 裡呼叫 setter / getter / instance methods
# 2. 宣告 class method 時
# 但是 self 本身是什麼？
class Person
  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end

  def greet
    puts "Hello, my name is #{self.name}"
  end
  # 用這個 method 把 self 印出來
  def who_am_i
    puts self
  end
end

bob = Person.new("bob", 17)
bob.who_am_i
# <Person:0x007ff1ba087dd0>  self 在 instance method 裡
# 是指呼叫 instance method 的 object
# 所以在 instance method 裡面 self.age = bob.age
```

```ruby
class Person
  attr_accessor :name, :age

  #今天我要是在class裡，instance methods 外看 self
  puts self

  def Person.info 
  end

  def initialize(name, age)
    @name = name
    @age = age
  end

  def greet
    puts "Hello, my name is #{self.name}"
  end
end

# => Person
# 所以在 class 裡面，instance method 外面，self 是指 class 自己
# 在在 class 裡面，instance method 裡面，self 是指被創出的某 object
```

```ruby
class Person
  attr_accessor :name, :age

  #今天我要是在class裡，instance methods 外看 self
  puts self

  def Person.info 
  end

  def initialize(name, age)
    @name = name
    @age = age
  end

  def greet
    puts "Hello, my name is #{self.name}"
  end
end

# => Person
# 所以在 class 裡面，instance method 外面，self 是指 class 自己
# 在在 class 裡面，instance method 裡面，self 是指被創出的某 object 
```

## Class Method
```ruby
# class 可以想像成是物件的模板/藍圖，但是他本身也可以被定義一些 method
class Person
  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end

  # 定義 class 自己的 method
  def self.hello
    puts "hello, i am Person Class"
  end
end

# 呼叫方式
Person.hello
#=> hello, i am Person Class
```

## Class Variable
```ruby
# 如果說 instance variable 是綁定物件的資料，那 class variable
# 就是綁定 class 本身的資料
class Person  
  attr_accessor :name, :age
  # 宣告時前面加兩個 @@
  @@number_of_people = 0

  def initialize(name, age)
    @name = name
    @age = age
    # 每創一個新的 object，就會被加一次
    @@number_of_people += 1
  end

  def self.hello
    puts "hello, i am Person Class"
  end
  # 回傳 @@number_of_people
  def self.info
    @@number_of_people
  end
end

puts Person.info
bob = Person.new("Bob", 17)
puts Person.info
# => 1
sam = Person.new("Sam", 32)
puts Person.info
# => 2
```

## Inheritance (繼承)
```ruby
# 我們希望在建立新的 class 時，新的 class 也包含了舊的 class 的方法和特性
# 這時就可以使用 inheritance(繼承)，讓我不用重新寫很多東西
class Person  
  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end

  def greet
    puts "hello, my name is #{self.name}"
  end
end
# 使用 < 來代表繼承
class Engineer < Person
  
end

class Salesman < Person

end

bob = Engineer.new("Bob", 17)
sam = Salesman.new("Sam", 32)
bob.greet
# => hello, my name is Bob
sam.greet
# => hello, my name is Sam
# Engineer 和 Salesman 繼承了 Person 的 greet 方法
```

## Homework
用物件導向重構剪刀石頭布遊戲  
https://github.com/yuyueugene84/lesson4/blob/master/RPS_OOP.rb  