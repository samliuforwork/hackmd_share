# 11/06(五)測試(重要), dcard開發, Migration
###### tags: `龍哥`

### Test-driver development (TDD)
* 測試白話來說，就是寫一段程式碼，驗證另一段程式碼可否運作，測試的目的並非debug。
* 本質上是一種開發流程，測試只是過程手段，重點該放在開發
* 先畫靶在射箭，先寫測試(規格)再寫程式
* 測試不存在的功能，假設其可以正常運作
* 測試兩大套件：minitest(Ruby內建，速度比較快但語法不清明), Rspec(比較多人使用，需要額外安裝)
* 先確定客戶需求才有辦法寫測試

### 測試3A原則
1. A = Arrange ，先把東西排好
2. A = Act ，操作
3. A = Assert ，確認操作真的成真

### 為什麼要寫測試？


### 軟體版本版號解說
3.10.0
3.8.0
6.1-rc1(Release Candidate)

Major(幾乎不會向下相容) / Minor(有可能不相容) / Patch(通常是修改小bug,安裝性 能夠向下相容)




#### 新提到觀念

* Singleton method 單體/單例方法 可以在任意物件中定義任意方法(少用)

Callback

before: 比較適合做初始化的事情，不適合用做變數宣告等

* 終端機rails c → "Person".pluralize

* SQL語法
User.all = select * from users;



```
class ATM
end

RSpec.describe ATM do
  context "存錢功能" do #拿來做目錄分類(context等同於describe)
    it "可以存錢" do
          # AAA
      # A = Arrange
      atm = ATM.new(10)

  # A = Act
  atm.deposit(5)

  # A = Assert
  # Matchers
  expect(atm.balance).to be 15  #(be(15)) 空白的地方省略了小括號

end
  end
end
```

### 15:00
# Dcard開發

User
    -has_many Boards
    -has_many Posts
    -has_many Comments
    
Cateogry
    -has_many Boards
    
Boards
    -has_many Posts
    -belongs_to Category

Post
    -has_many Comments
    -belongs_to User
    -belongs_to Board
    
Comment
    -belongs_to Post
    -belongs_to User

-會員系統
    -email/password
    -nickname
    -account
    -avatar
    -school
-看板
    -分類
    -名稱
    -文章s
        -title
        -content
        -作者
        -回應s
            -
            ![](https://i.imgur.com/nMfK1Qz.jpg)

* 若post是Belong to某個board，則要以board.id來註解出自於哪裡
* rails d model 如果在generate打錯的時候可以砍掉


### 16:10

### Migration
描述說接下來這個表格長什麼樣子，migration是table的記錄成長表，是要進入版本控制裡面的，做過一次就不會再做第二次。(記得在migration前確定檔案有存檔，若migration到空的表格就麻煩，因為rollback是砍表格，但沒表格要怎麼砍。此時最好去檢查schema.rb因為都有紀錄)
* rails db:rollback 把執行的db倒回去
* rails db:rollback STEP=3