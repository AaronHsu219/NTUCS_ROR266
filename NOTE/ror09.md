# 課程大綱
Lesson 1 & 2 : 安裝環境 & Ruby 語法  
Lesson 3 : Ruby 與物件導向  
Lesson 4 : MVC 架構與資料庫  
Lesson 5 & 6 : Rails Model與ActiveRecord    
Lesson 7 & 8 : Rails 表單與 Heroku 上架  
Lesson 9 & 10 : 使用者註冊與登入  
Lesson 11 & 12 : Bootstrap 美化網站  

## 著名Rails專案
* airbnb
* twitch
* GitHub
* slideshare
* KKTIX
* Inside

## 展示一下 Rails 的魔力
```ruby
rails g scaffold order name:string phone:string description:text
```

## Hello World!
```ruby
string = "Hello World!"
puts string
```

## String (字串)
```ruby
# 宣告一個 string (字串) 這樣做，記得字串一定要包在 " " 裡面

str = "Welcome to NTU Rails 261!"

# 若要把兩個 string 接在一起，可直接用加號 + 

str1 = "Welcome to"
str2 = " NTU Rails 261!"
# irb 輸入
str1 + str2
# 就會得到：
# Welcome to NTU Rails 261!
# 用 puts 印出結果:
puts str1 + str2
```
```ruby
# 但是用 + 號連接字串會多耗記憶體，所以我們可以用字串內差(string interpolation)的方式連接字串
# 用法就是 "#{這邊放你的字串或數字}"

# irb 輸入:
str1 = "Welcome to"
str2 = " NTU Rails 26ˊ!"
puts "#{str1}#{str2}"

# 會得到 Welcome to NTU Rails 266！

# ruby 字串也會包含型別轉換，所以你若是從 gets.chomp 得到字串型別的數字

number_str = "5"

# 你就可以用 .to_i 把這個字串轉成整數

number_str.to_i

# 會得到 5
```
##印出字串
```ruby
# print 是把任何物件轉成字串印出

number = 5
string = "Hello"

print numer
print string

# =>5string

# puts 是把任何物件轉成字串，加上斷行，再印出

number = 5
string = "Hello"

puts number
puts string

# =>5
# =>Hello
```

## 數字
```ruby
# 數字主要分為整數與浮點數
# 1, 101, 888 為整數

# 檢查資料型別的方式: 用 .class
1.class 
# =>Fixnum

# 0.05, 3.14, 0.00001 是浮點數
(3.14).class
# =>Float

數字可用 to_s 轉成字串
5.to_s 
# =>"5"
```
## 數字運算
```ruby
# 加法
1 + 1
# => 2

# 減法
2 - 1 
# => 1

# 乘法
3 * 3
# => 9

# 除法
9 / 3
# => 3

# 餘數
10 % 3
# => 1

# 平方
2 ** 3
# => 8
``` 

## Boolean (布林值)
```ruby
# true 和 false 是布林值，是電腦用來表示 '對'' 和 '錯' 的資料型別

1 == 1 

# => true

1 == 2

# => false
```

## Array (陣列)
```ruby
# 陣列(array) 可以把它想像成儲存許多值的清單，你可以：
arr = [1,2,3,4,5,6,7,8,9] # 把 1 到 9 存在 arr 這個陣列裡

# 也可以在裡面塞很多不同型別的資料：

arr2 = [0.3, "ntu rails", 4]

# 你也可以在 array 裡面塞另一個 array:

arr3 = [1, 2, [3,4]]
```
```ruby
# 今天我要取得裡面儲存的值時，就需要他的索引值(index)
arr = [1,2,3,4]
arr[1]

＃ =>2
# 注意索引值是從 0 開始算起

arr  =   [1,2,3,4,5,6,7,8,9]
#索引值：  0 1 2 3 4 5 6 7 8 

#所以我要是希望在 arr 裡面取得 1：

arr[0] = 1

#就需要去index 為 0 的地方取得

#若是要刪掉 index 為 2 的值

arr.delete_at(2)

#然後 arr 裡面的 3 就被刪掉了
[1,2,4,5,6,7,8,9]
```
```ruby
# 今天我若要把 array 的最後一個值刪掉：
arr = [1,2,3,4,5,6,7,8,9]
arr.pop 

# 就會把 9 移除

# 若要把 9 加回 array 最後面：

arr.push(9)

# 也可以這樣寫：

arr << 9 # 非常簡潔易懂
```
```ruby
# 最後，我想檢查一個 arr 裡是否存在 5：
# 可以用 include? method
arr = [1,2,3,4,5,6,7,8,9]

arr.include?(5)
# 5 存在，所以會回傳 true，相對的

arr.include?(18)
# 會回傳 false
```