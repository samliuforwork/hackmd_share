# 11/09(一)Rails 新增修改刪除 
###### tags: `龍哥`

### bundle install與gem install差異
bundle install 跟 gem install都是安裝一份套件，budle install後面是gem install，但bundle install會讀取gemfile有哪些gem後才安裝套件，並且將更新gem的版本到gemfile.lock

![](https://i.imgur.com/tX3mSi0.png)

使用框架的最大目的：有一套慣例，大家可以用共同的語言理解
REST 是 Representational State Transfer 的縮寫，中⽂翻譯成「具象狀態傳輸」，它是由 Roy Thomas Fielding 博⼠在 2000 年時提出的軟體架構。簡單的說，就是把每個網址當做資源（Resource）來看待，對同⼀個資源做不同的動作（HTTP Verb）會得到不同的結果。符合 REST 概念設計的網址，⼜稱之 RESTFul Route。

  get '/boards', to: 'boards#index'
  進入boards路徑，在boards控制器裡面的index動作
  
  靜態頁面可以編列一個pages控制器
  
  ![](https://i.imgur.com/IijB9iS.png)
下面的寫法可以一次全部改，需求變更較為容易，上面那個要一個一個改(在routes可以加入path更改)，但是下面那行效能運作些微較差(因為是方法)

### 相同路徑的寫法，最推薦第四個  (View helper)
<a href="/boards/new">新增看板</a>
<a href="<%= new_board_path %>">新增看板</a>
<%= link_to "新增看板", '/boards/new' %>
<%= link_to "新增看板", new_board_path %>

![](https://i.imgur.com/qWmAqaf.png)
表單action的預設為空字串(他就會自己跳)，method預設方法為get

# 13:53
![](https://i.imgur.com/Hkoa9ki.png)
POST跟GET最大差別在於傳送資料的方式不同。
POST:欄位的傳送會到HTTP的Require body裡面，用POST稍微比較隱密。
GET:欄位的傳送會以「?」以及「&」傳送到網址路徑，帳號密碼會出現在網址中，他人使用瀏覽紀錄就能看到。

![](https://i.imgur.com/aXlAndm.png)
如果要將資料傳到後端，會抓name

params:使用者傳遞過來的東西

https://zh.wikipedia.org/wiki/%E7%BB%9F%E4%B8%80%E8%B5%84%E6%BA%90%E5%AE%9A%E4%BD%8D%E7%AC%A6

https://en.wikipedia.org/wiki/URL
![](https://i.imgur.com/A8KXSIP.png)

http://
- protocal

localhost
- hostname/domain name

/boards/new
-path -> routes.rb

?id=2&name=3&cc=4
-querystring -> params 的一部分

![](https://i.imgur.com/wAwNY60.png)
等號代表把東西輸出

    @board.title = params["board"]["title"]

    params = {
      "board" => {
        "title" => "..."
      }
    }
    
跟商業驗證有關、容易重複使用的盡量寫在model裡面

class BoardsController < ApplicationController
  def index
  end

  def new
  end

  def create
    clean_params = params.require(:board).permit(:title)
    @board = Board.new(clean_params)

    if @board.save
      redirect_to "/"
    else
      render :new  # render 'boards/new'
    end
  end
end

### Render是借new檔案來用