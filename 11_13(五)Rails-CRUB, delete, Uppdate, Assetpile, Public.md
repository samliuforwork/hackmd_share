# 11/13(五)Rails-CRUB, delete, Uppdate, Assetpile, Public
###### tags: `龍哥`

### 補充觀念
##### 如何追出rails中方法的定義
* method(:notice).source_location
https://kaochenlong.com/2011/08/09/how-to-find-a-method-definition-in-ruby/

* 只有view而沒有給action其實會給過，但不太建議這麼做

### AssetPile觀念
* application裡面的manifest是負責做打包，把渣渣、空白壓縮，減少檔案大小以及request的數量。
* *= require_tree . 這個會把這個目錄下(含子目錄)所有CSS的require進來，不包含application自己裡面。
* 但在打包成一個檔案時，如果class重複使用則要考慮到先後順序、優先權問題
* require的資料夾可以用frontend/backend...等命名。 
* Asset pipepline與webpack兩套都要學，但擇一使用。(舊專案仍以asset pipeline為主，可能是以後工作要面對的)

![](https://i.imgur.com/0v2WXqm.png)

<!DOCTYPE html>
<html>
  <head>
    <title>ZCard</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <p><%= flash["notice"] %></p>
    <%= yield %>
  </body>
</html>

### 巧思
  <body class="<%= controller_name %>-<%= action_name %>">
  會自動依照controller, action來命名，就不用擔心打包時命名衝突


### Partial Render(局部渲染)
##### 觀念
* 好處是可以整理程式碼，並控制決定使用者在畫面上看到的東西

##### flash的同義寫法
    <%= render "shared/flash" if flash[:notice] %>
    <%= render "shared/flash" if flash["notice"] %>
    <%= render "shared/flash" if notice %>



##### Unobrusive javascript(非侵入式javascript)
![](https://i.imgur.com/e8bnU96.png)



### public資料夾
![](https://i.imgur.com/ceps6T8.png)
* 404頁面其實存在，放在public底下的皆不需要經過routes, MVC。
* Asset裡面、圖片等也通常會放進public，若連圖片都要經過MVC未免也太耗時。

#### 如何注意細節的處理404頁面
```
  def hello
    render file: 'public/404.html',
           layout: false,
           status: :not_found
  end
```
# 編輯

#### before_action等同於filter_action

#### rails裡面如果要看單筆資料的路徑(跟show有關的路徑)，則board_path(board.id)可以省略成board_path(board)，又可在省略成board。
```
board_path(board.id)
board_path(board)
board
```



#### 14:06

#### 影片
find_by! 14:52

