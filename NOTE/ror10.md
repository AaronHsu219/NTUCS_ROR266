## 基本的 Unix 指令
```ruby
# mkdir 是創出一個新的路徑(也就是資料夾)
mkdir ntu_ror_266

# cd 是改變路徑到某個地方
cd ntu_ror_266 

# ls 是把目前這個目錄下的所有檔案都列出來
ls

# => ntu_ror_266

# touch 是創造一個新的檔案
touch hello_world.rb

# subl 是開啟 sublime
subl hello_world.rb
subl .

# ruby 是執行副檔名為 .rb 的檔案
ruby hello_world.rb
```

## Unix 指令教學
http://linux.vbird.org/linux_basic/redhat6.1/linux_06command.php

## git 版本控制
https://github.com/yuyueugene84/ntu_ror_training_course/blob/master/learn_git.md

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
```ruby
加法
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
true 和 false 是布林值，是電腦用來表示 '對' 和 '錯' 的資料型別

1 == 1 

# => true

1 == 2

# => false
```
## Method
```ruby
# method 方法，我們經常遇到一個程式裡面會有許多不斷重複的程式碼，我們可以把它們打包起來使用
# 可以把 method 想像成數學公式：X + Y = Z，你只要輸入 X 和 Y，這個公式就可幫妳算出 X 和 Y 的和，也就是 Z
# 若我們今天需要寫一個經常會用到計算園面積的程式，我們就可以把計算園面積的程式碼寫成一個 method:

# 宣告程式要用 def 關鍵字，加上你幫 method 取得名字，這裏我幫它取名叫 area_of_circle
def area_of_circle(radius) # (你要丟給方法的輸入，也就是參數，要寫在括弧裡)
  return radius * radius * 3.14 # 計算式，注意你要計算的變數需要和括弧裡你設定的參數名一樣
end

# 我接下來可在程式任何一個地方呼叫我的方法
cicrle1 = area_of_circle(3)
irb(main):015:0> cicrle1 = area_of_circle(3)
# 放進 irb 裡面算，就可得出半徑是 3 的圓面積
# => 28.26
```
```ruby
# 我也可以呼叫很多次
circle2 = area_of_circle(5)
# => 78.5
circle2 = area_of_circle(8)
# => 200.96
circle2 = area_of_circle(10)
# => 314.0

# 我也可以算長方形的面積
def area_of_rectangle(width, height) # 這時我就需要兩個參數，寬與高
  return width * height
end

# 呼叫它的方法就是
area_of_rectangle(5,6) #(傳進兩個參數)
# => 30
```

## Comparisons (邏輯運算) [LaunchSchool](https://launchschool.com/books/ruby/read/flow_control#comparisons)
```ruby
# 電腦用來代表對和錯，是或否的資料型別是
true 
false

# 他們叫做布林值(Boolean)

# 另外，nil 則是 ruby 用來表示空值的資料型別
nil

# 若想知道一個變數是否為空值，可用 nil? 方法
var = nil # 設定 var 為 nil

var.nil? # 變數 var 是否為空值？
#=> true 
# 回傳 true，代表 var 是空值

# A == B 是比較 A 和 B 是否相同
if 5 == 5
  puts "5 等於 5"
end
```

```ruby
# A != B 是比較 A 和 B 是否不同
if 4 != 5
  puts "4 不等於 5"
end

# A < B 是比較 A 是否小於 B
if 4 < 5
  puts "4 小於 5"
end

# A > B 是比較 A 是否大於 B
if 5 > 4
  puts "5 大於 4"
end

# A >= B 是比較 A 是否大於等於 B
if 5 >= 4
  puts "5 大於等於 4"
end
```

```ruby
if 4 >= 4 #若這樣比
  puts "5 大於等於 4" #這行也會被印出
end

# A <= B 則是比較 A 是否小於等於 B

if 5 <= 6
  puts "5 小於等於 6"
end

if 6 <= 6 #若這樣比
  puts "5 小於等於 6" #這行也會被印出
end
```

```ruby
# A && B 則是指 A 必須成立而且 B 也必須成立，我才會回傳 true
if (4 < 5) && (5 < 6)
  puts "兩者都成立"
end

if (4 < 5) && (5 > 6) #這樣就不會印出任何東西，因為( 5 > 6 )不成立
  puts "兩者都成立"
end

# A || B 則是指只要 A 或 B 其中一方成立，我就會回傳 true
if (4 < 5) && (5 < 6) #這樣會印出東西，因為兩者皆成立
  puts "兩者都成立"
end

if (4 < 5) || (5 > 6) #這樣也會印出東西，因為兩者其中一方成立
  puts "兩者都成立"
end
```

```ruby
# !A 則是取身為布林值 A 的反值，所以
!(4 < 5) #放入 irb 裡會回傳 false, (4 < 5) 會回傳 true, 但前面加的 ! 會取 true 的相反值，也就是 false

# 在 ruby 裡，變數前面有兩個驚歎號代表會把判斷這個變數是否有值

!!5 
# =>true  5並非空值

str = "p"

!!str 
# =>true str, 也就是"p"，並非空值

# ruby 語言裡唯二會被判斷成 false 的值分別是 false 和 nil
!!false
# => false
!!nil
# => false
```

```ruby
# ternary operator 簡單來說，就是讓你用更簡潔的方法來寫 if...else 判斷式
# 語法是 判斷式 ? 成立要執行或回傳的程式碼 : 不成立要執行或回傳的程式碼

puts true ? "true" : "false"
# => "this is true"


puts false ? "true" : "false"
# => "this is false"
```

## Condition(判斷式)
```ruby
input = 6

if input < 5 # 如果 if 後面判斷式成立 
  puts "#{inpurt} is less than 5" # 就執行這邊
else # 不成立的話
  puts "#{inpurt} is greater than or equal to 5" # 只好執行這邊
end

# => 6 is greater than or equal to 5
```

```ruby
operation = 3

if operation == 1 #判斷式不成立，會接下去看下一個 elsif
  result = num1 + num2
  puts "your answer is: #{result}"
elsif operation == 2 #判斷式還是不成立，會接下去看下一個 elsif
  result = num1 - num2
  puts "your answer is: #{result}" 
elsif operation == 3 # 成立!，印出 num1 x num2 的結果
  result = num1 * num2
  puts "your answer is: #{result}"
else 
  result = num1.to_f / num2.to_f
  puts "your answer is: #{result}"
end
```

```ruby
# case...when，用敘述來測試一連串條件

operation = 5

case operation #case 關鍵字後面要加上被判斷的變數

when 1 # 到這裡，ruby 會去判斷 when 後面的參數是否等於 case 後面的變數
       # 就等同於執行 operation == 1 (但請不要把判斷式寫在這裡喔)
  puts "operation is equal to 1" # 若 operation 等於 when 後面的結果，執行這段程式碼
when 2 # 到這裡，ruby 會去執行 operation == 2
  puts "operation is equal to 2" # 若 operation 等於 when 後面的結果，執行這段程式碼，以此類推
when 3 # 以此類推...
  puts "operation is equal to 3"
when 4 # 以此類推...
  puts "operation is equal to 4"
else # 預設項目，若上面所有的 case 都不成立時，就執行預設項目裡的程式碼
  puts "operation is equal to 5"
end
```

```ruby
# when 後面要被比較的結果也可以是字串 
operation = "3"

case operation #case 關鍵字後面要加上被判斷的變數

when "1" # 到這裡，ruby 會去執行 operation == 1 (請不要把判斷式寫在這裡喔)
  puts "operation is equal to 1" # 若 operation 等於 when 後面的結果，執行這段程式碼
when "2" # 到這裡，ruby 會去執行 operation == 2
  puts "operation is equal to 2" # 若 operation 等於 when 後面的結果，執行這段程式碼，以此類推
when "3"
  puts "operation is equal to 3"
when "4" 
  puts "operation is equal to 4"
end
```

```ruby
# 當然，Ruby 是講求程式碼精簡的語言，所以我們可以把 case when 的程式碼變得更簡潔一點：

operation = 3

case operation 
when 1 then puts "operation is equal to 1" # 加上 then 關鍵字，可直接把要執行的程式碼寫在 then 後面
when 2 then puts "operation is equal to 2" 
when 3 then puts "operation is equal to 3"
when 4 then puts "operation is equal to 4"
end
```

## Loop(迴圈)
```ruby
3.times do 
  puts "Hello World!"
end

#代表這個會印出三次 "Hello World!" 

# while loop 則是會根據 while 後面的判斷式決定是否要繼續執行迴圈
# 可以想成 '只要' 條件式還成立，我就繼續執行

# 要先給 i 個起始值
i = 10

while i > 0 #判斷式是只要 i 大於 0，我就繼續執行
  puts "while loop to #{i}"
  i -= 1 #每執行一次，i 就會減一，這就是所謂的"遞減"
  #若這邊比較難看懂，可以把 i -= 1 想像成 i = i - 1
end
```

```ruby
# begin...end while 和 loop do 一樣，主要是用於一些我不知道起始值的狀況

begin #告訴電腦先執行以下程式碼，而不是先判斷

  puts "輸入 5 才能退出喔" #讓電腦印出問題
  input2 = gets.chomp.to_i #讀取使用者的輸入，用 to_i 轉成整數 

end while input2 != 5 #判斷式寫在最下面，只要 input2 不等於 5，我就回到上面繼續執行
```

## Symbol (符號)
```ruby
# 宣告時在前面加 : 符號，可以想像成識別符號

:name

# symbol vs string

#string 可以被改變，但 symbol 不能被改變

"hello" + " world"

# =>"hello world"

:hello + :world

# => NoMethodError: undefined method `+'
```

## Array (陣列)
```ruby
# 陣列(array)是一種資料結構，可以把它想像成儲存許多值的清單，你可以：
arr = [1,2,3,4,5,6,7,8,9] # 把 1 到 9 存在 arr 這個陣列裡

# 也可以在裡面塞很多不同型別的資料：

arr2 = [0.3, "ntu rails", 4]

# 你也可以在 array 裡面塞另一個 array:

arr3 = [1, 2, [3,4]]
```

```ruby
# 今天我要取得Array裡面儲存的值時，就需要他的索引值(index)
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
今天我若要改變 array 裡面所有的值，像是把所有值加上 2

arr.map {|x| x + 2} #使用 map 方法，x 代表每一個值

# 執行後，就會得到：

[3, 4, 5, 6, 7, 8, 9, 10, 11]

# 但這不會改變 arr 裡面原本的值，但若我們用 map!

arr.map! {|x| x + 2}

# 再查看一次 arr，此時 arr 就被改變了

arr = [3, 4, 5, 6, 7, 8, 9, 10, 11] 

# 任何加 ! 的方法代表呼叫該方法的物件最後會被改變
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
最後，我想檢查一個 arr 裡是否存在 5：
# 可以用 include?

arr = [1,2,3,4,5,6,7,8,9]

arr.include?(5)
# 5 存在，所以會回傳 true，相對的

arr.include?(18)
# 會回傳 false
```

##　取得使用者輸入
```ruby
# 取得使用者在 command line 上面輸入的值

input = gets.chomp
```

## Debugging
```ruby
# 使用一個叫做 pry 的套件

gem install pry

# 在每一個 .rb 檔最上面加上

require 'pry'
```

## Hash (雜湊)
```ruby
# 另一種資料結構，可以把他想像成置物箱，每一個值(value)會對應到一個鑰匙(key)

person = { 
           :name => "Bob", 
           :age => 30,
           :occupation => "Engineer"
         }

# 在上面的範例，:name, :age, :occupation 是 key，"Bob", 30, "Engineer" 是 value
# 因為 symbol 是 immutable (不能被改變的)，所以很適合用來當做 key
# 若我要取得某個 value，我需要它的 key

person[:name] 

# => "BOb"
``` 

```ruby
# ‘=>' 符號叫做 hashrocket，是 hash 用來 assign 值所使用的符號
# 但是 Matz 老大認為 hashrocket 讓 hash 看起來太醜了...
# 所以在未來新版的 Ruby 裡，hashrocket 會逐漸的被淘汰
# 新的 hash 宣告方式 

person = { 
           name: "Bob", 
           age: 30,
           occupation: "Engineer"
         }

# 目前 Ruby 是兩種寫法都支援
```

## Range (範圍)
```ruby
# range 可以聯想成範圍 
  1..10 #代表 1 到 10
# 另一種 range
  1...10 #(中間有三個 ...) 代表 1 到 9

# 放進 irb 執行：
# irb(main):003:0> (1..10).to_a #把它轉成 array 比較容易看懂
# => [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] # 1 到 10
# irb(main):004:0> (1...10).to_a 
# => [1, 2, 3, 4, 5, 6, 7, 8, 9] # 三個 . 的範圍只從 1 到 9
```

## Random(隨機)
```ruby
# 我們有些時候會需要電腦幫忙產出隨機數(可以想像成骰子)，ruby 就有提供一個這樣的一個功能：

rand(1..100) #會產生出一個介於1到100之間的隨機數，記住裡面要放入的是一個 range 
# => 33
# => 87
# ...

# array 也有類似的功能， shuffle (洗牌)

arr = [1,2,3]

arr.shuffle!
# => [1, 2, 3]
arr.shuffle!
# => [3, 2, 1]
arr.shuffle!
# => [1, 3, 2]
arr.shuffle!
# => [3, 2, 1]

# 記住 shuffle! 和 shuffle 的差別在於只有 shuffle! 會改變 arr 的資料
```

## Homework
剪刀石頭布  
https://github.com/yuyueugene84/lesson2/blob/master/homework1.rb