## Quiz 1 Solution
計算機程式碼  
https://github.com/yuyueugene84/simple_calculator/blob/master/calculator_method.rb

## 今天上課的程式碼
https://github.com/yuyueugene84/ntu_ror_266_lesson4  

## Constants (常數)
```ruby
# constant 就是有些時候會遇上一些在程式裡不應改變的變數
# 像是圓周率、法定成年的年紀 etc.
class Person  
  # 宣告 constant，全部大寫
  LEGAL_AGE_TO_DRIVE = 18
  PI =  3.1469680

  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end
  # 看這個人是否已到可以考駕照的年齡
  def can_drive?
    if self.age >= LEGAL_AGE_TO_DRIVE 
      puts "yes #{self.name} can drive"
    else 
      puts "no #{self.name} can't drive"
    end
  end
end

bob = Person.new("Bob", 17)
bob.can_drive?
#=> yes Bob can drive
```

## Module (模組)
```ruby
# 可把 module 想像成工具箱，本身並不是 class
# 不可 new，只能被 include 到其他 class 裡面使用
module Knowledge
  def program
    puts "I know how to program"
  end
end

class Person  
  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end
end

class Engineer < Person
  include Knowledge
end

bob = Engineer.new("Bob", 17)
bob.program
# => I know how to program
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

## Inheritance vs Module
```ruby
1. You can only subclass from one class. But you can mix in as many modules as you'd like.  
   你只能為一個 class 建立子類別，但卻可以 mix 很多 module  

2. 如果今天你是需要 "是某個..." 的關係，就用 inheritance，如過需要 "擁有某項行為" 就用 module  
   Ex. 狗是屬於一種動物，就讓 Dog 繼承 Animal  
       狗有游泳的能力，就讓 Dog include 擁有 swim 這個 method 的 module  

3. Module 不能使用 new，他只能被其他 class 使用  
```

## Method Override (覆寫)
```ruby
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
# 如果我希望在改變 Engineer 的 greet
class Engineer < Person
  # override (覆寫) 原本 Person 的 greet
  def greet
    puts "I am an Engineer, my name is #{self.name}"
  end
end
# 創立一個叫 German 的子類別
class German < Person
  # override (覆寫) 原本 Person 的 greet
  def greet
    puts "Hallo, mein name ist #{self.name}"
  end
end
bob = Engineer.new("Bob", 17)
martin = German.new("Martin", 20)
bob.greet
martin.greet
#=> I am an Engineer, my name is Bob
#=> Hallo, mein name ist Martin
```

##　Super
```ruby
class Person  
  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end

  def greet
    "hello, my name is #{self.name}"
  end
end
# 如果我希望在改變 Engineer 的 greet
class Engineer < Person
  # override (覆寫) 原本 Person 的 greet
  def greet
    # super 會呼叫 parent class 裡面同樣名字的 method
    # 注意 super 只能在 method 裡面使用
    puts super + ", I know how to write Ruby"
  end
end

bob = Engineer.new("Bob", 17)
bob.greet
#=> hello, my name is Bob, I know how to write Ruby
```

## Method Lookup 
```ruby
module Knowledge
  def program
    puts "I know how to program"
  end
end

class Person  
  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end
end

class Engineer < Person
  include Knowledge
end

# 尋找 Engineer 的祖先們
puts Engineer.ancestors

# Engineer
# Knowledge
# Person
# Object
# Kernel
# BasicObject

# 一旦 object 呼叫了一個它的 Class 裡面沒有的 method
# 他就會依序找他所有的祖先，若找到了有這個 method 的祖先，就使用這個祖先類別的 method
```

## Public Method
```ruby
# method 有三種不同的權限
# public 就是任何屬於這個 class 的物件都能使用

class Person 
  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end
  # greet 就是 public method
  def greet
    puts "hello, my name is #{self.name}"
  end
end

bob = Person.new("Bob", 30)
bob.greet

#可以在程式的任何地方被使用
```

## Private Method
```ruby
# private 是只有在 class 內部才可以存取
# 適用於有些時候，你希望一些 method 不會被程式的其他地方使用到(像是金流、身分證字號 etc.)
class Person  
  attr_accessor :name, :age
  def initialize(name, age)
    @name = name
    @age = age
  end

  def identity
    #只能在 class 裡面被其他 instance method 呼叫，前面不能加 self
    puts "secretly, #{secret_method}"
  end

  private # 先寫 private 關鍵字
    def secret_method
      "I am Iron Man!"
    end
end

bob = Person.new("bob", 17)
bob.identity
# secretly, I am Iron Man!
# private method 不可直接被物件呼叫
bob.secret_method
#=> private method `secret_method' called
#=> for #<Person:0x007ff182033498 @name="bob", @age=17> (NoMethodError)
```

## Protected Method
```ruby
# protected 是介於 public 和 private 之間
# 從 class 外面來看，protected 就像 private，不能被物件直接呼叫
# 從內部看 protected method 可被其他 instance method 呼叫，就像一般的 public method
class Person  
  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end

  def identity
    #在 class 裡面可被其他 instance method 呼叫
    puts "secretly, #{protected_method}"
  end

  protected # 先寫 protected 關鍵字

    def protected_method
      "I am Spider Man!"
    end
end

bob = Person.new("bob", 17)
bob.identity
# secretly, I am Spider Man!
bob.protected_method
# => protected_class.rb:31:in `<main>': protected method `protected_method' called for
# => #<Person:0x007fb9f3033428 @name="bob", @age=17> (NoMethodError)
```

## OOP Design Pattern
要如何封裝我的資料？  
如何設計我的 class  
一個 class 該有什麼行為、該具備哪一些責任  
如何設計一個能夠適應改變的程式  

## SQLite Browser
如果你是用 Mac：  
http://sqlitebrowser.org/   

如果你是用 Ubuntu：  
https://apps.ubuntu.com/cat/applications/sqlitebrowser/  

## Relational Database (關聯式資料庫)
看資料庫是如何透過關聯把多個資料表結合起來：  
http://sqlbolt.com/lesson/select_queries_with_joins  

## Extra
HTML & CSS 練習  
https://www.codecademy.com/learn/web  
http://www.w3schools.com/  
http://www.w3school.com.cn/  ​ 

### Ruby 語言練習
https://www.codecademy.com/learn/ruby  

### SQL 語言練習
https://www.codecademy.com/learn/learn-sql  
http://sqlbolt.com/  
