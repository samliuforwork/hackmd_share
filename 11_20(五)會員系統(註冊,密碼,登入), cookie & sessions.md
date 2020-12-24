# 11/20(五)會員系統(註冊,密碼,登入), cookie & sessions
###### tags: `龍哥`

#### 觀念

#### form_for(model) & form_tag(url)
* 簡單計算BMI，用不到model...使用form_tag即可
* form_with的作用是取代上面這兩者
* * form_with(model @user)
* * form_with(url: '/')
* form_for是整列資料往外打出去
* form_with是以AJAX方式送出，為了提高UX(google map就是個好例子)，`<form action="/messages" method="post" data-remote="true">`
上面程式中，form_with的data-remote="true"，代表著預設為表單透過Ajax提交；如果不要設定Ajax提交，則要另訂 local: true。

#### Turbolink
* 做網頁時，有一些網頁切換頁面時頭尾不變
* Turbolink時，使用AJAX技術將中間的肉從B塞到A，在把A網頁更改名稱為B
[* 深度研究turbolink](https://www.writershelf.com/article/rails-turbolinks%E2%84%A2-5-%E6%B7%B1%E5%BA%A6%E7%A0%94%E7%A9%B6?locale=zh-TW&prne=roa)

##### Cookie
* 買飲料訂單給的號碼牌，去別家飲料店沒用。這就是為什麼每次登陸fb它都記得我的帳號密碼。是瀏覽器存放資料的地方，可以存放seesion之類的資料

##### Sessions
* session透過cookie去儲存uniqueID，透過session ID傳遞至URL比較不安全，因此必須透過cookie
* 後台伺服器，經過核對您手上的cookie，確定是你號碼。帳號登錄驗證過後，Server端所發的識別證。
* 假如session沒存放重要資料且不需要持續長久，可以考慮使用ActionDispatch::Session::CacheStore
* sessions預設為Lazy Loading
> Lazy loading 是指從一個資料物件通過方法獲得裡面的一個屬性物件時，這個對應物件實際並沒有隨其父資料物件建立時一起儲存在執行空間中，而是在其讀取方法第一次被呼叫時才從其他資料來源中載入到執行空間中，這樣可以避免過早地匯入過大的資料物件但並沒有使用的空間占用浪費。
* 使用者登入的這個狀態，是同時建立在使用者手上持有cookie以及被伺服器承認兩個要件成立之上。
* * 本地Memory，需要耗的資源小、存取
* * Memory Server(Redis) 檔案可以存在本地硬碟，需要時在叫出來
* * Database，開一個資料表專門放這些，重開機不會消失，因為每次存取資料都要跟資料庫要，因此速度較慢

* delete其實是偽裝的POST，使用POST的話網頁會檢查token

[Day14-Session與Cookie差別](https://medium.com/tsungs-blog/day14-session%E8%88%87cookie%E5%B7%AE%E5%88%A5-eb7b4035a382)
https://github.com/aszx87410/blog/issues/46
* 

### 會員註冊

#### 會員密碼
* 會員註冊的密碼通常都需要加密
* 如果查詢的到的密碼，代表資料庫存有會員的密碼，因此也就是說密碼沒有加密

![](https://i.imgur.com/AI684on.png)
* 因為路徑是我們自己打的，form_for猜錯使得我們需要這樣用(因為我們不是用resources產生出來的)

##### 如何讓密碼變成******，同時密碼需填寫兩次
* <%= form.password_field :password %> (讓密碼變成******)
* ![](https://i.imgur.com/GYO3nqN.png)

* https://guides.rubyonrails.org/active_record_validations.html
* rails valida

###### model驗證，因為可能有長度限制，所以分開寫有彈性
![](https://i.imgur.com/cj4H2YM.png)

* 如果在rails裡面欄位叫做password，則在rails console中會看不到，但是其實還是能在資料庫中看到。

##### 如何幫密碼加密？
* 加密寫在哪？如果寫在controller上會難以重複使用，因此多寫在model裡
##### Callback：當發生或完成什麼事情時，call我一下
![](https://i.imgur.com/gVlEhVV.png)
* 加密要掛在before create!，若掛在before save則在更新資料時密碼也會被洗一次，不應該一直被觸發。

![](https://i.imgur.com/sNKHKmR.png)

##### 加密演算法的選擇
[參考資料API-ActiveSupport::MessageEncryptor](https://api.rubyonrails.org/classes/ActiveSupport/MessageEncryptor.html)
https://ruby-doc.org/stdlib-2.5.1/libdoc/digest/rdoc/Digest.html

* md5，已經被破解了
* 使用SHA-1
* 撒鹽：是指在雜湊之前將雜湊內容（例如：密碼）的任意固定位置插入特定的字串。這個在雜湊中加入字串的方式稱為「加鹽」。其作用是讓加鹽後的雜湊結果和沒有加鹽的結果不相同，在不同的應用情景中，這個處理可以增加額外的安全性。(頭尾加上a跟z)
![](https://i.imgur.com/LTGjiC6.png)
##### email regular expression
* format: { with: /[\w]+@([\w-]+\.)+[\w-]{2,4}/ }

### 會員登入

#### 使用者成功登陸了，如何判斷它成功登陸了，並且將登入字樣切換為登出
1. 發號碼牌，發cookie同時在伺服器創立session!(在Controller裡)
* ![](https://i.imgur.com/nImKe61.png)

2. 登入的這件事，伺服器需要判斷使用者手上是否持有cookie
* ![](https://i.imgur.com/JPEbVkL.png)

* 使用者有登錄的話，會給予伺服器資料，若沒有登陸則是回傳nil物件。藉由得到的物件來判斷使用者是否有登錄。

