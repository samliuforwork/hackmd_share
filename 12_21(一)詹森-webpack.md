# 12/21(一)詹森-webpack
###### tags: `JavaScript` `Workshop`

### 觀念
* 到bootstrap找樣式代碼複製
* 終端機輸入yarn add bootstrap
* boostrap會更新到node_modual裡
* webpacker打包的檔案，從網頁原始碼的network檢查所套用結果，記得按Preview，view裡的layout的apllication.html.erb可以看
* 去public裡面看，快捷鍵VScode ctrl+A+2
* application.js裡面的import 'bootstrap'
* 從console裡面看，缺少什麼裝什麼。
* 參考龍哥的文章，https://kaochenlong.com/2019/11/22/webpacker-with-rails-part-2/
* 只有在node.js的環境下才能使用import寫法，erb裡面不能寫import，只能寫require
* 今天只有改form_html.erb、application.js

---

## 詹森筆記

### yarn add 套件
- 更新 package.json
- 在 node_modules 下加入套件

### import 套件
- 在 application.js 內引入套件

> import 後可能只有 js 這時候可以去 node_modules 下去找 css


### import XX from 套件
- 譬如要用 jquery 的 $ 時 


### 怎麼樣可以知道 import 的路徑呢？
建議直接看 webpack 產生的 application.js，也可看該套件的 package.json，以 bootstrap 的 (package.json)[https://cdn.jsdelivr.net/npm/bootstrap/package.json] 他的 main 就是寫 
```
main: "dist/js/bootstrap"
```
也就是找
```
node_modules/bootstrap/dist/js/bootstrap.js
```



### js 寫在 body 跟 header 有什麼差別？

```html
<!DOCTYPE html>
<html>
  <head>
    <title>JsWorkshop2</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <%= render 'layouts/messages' %>
    <%= yield %>
  </body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
  <head>
     js 寫 header
  </head>
  <body>
    js 寫 body
  </body>
</html>
```


### 寫在 header 的 js 有 $ 但寫在 body 的沒有？

打包後的 $ 就像 function 裡的變數，只在 function 裡面有效

```js
// function 外面看不到裡面的變數
function test(){
  var a = 10
}

test()

console.log(a)
```

```js
// function 裡面看的到外面的變數
var a = 10

function test(){
  console.log(a)
}

test()
```

## 要怎麼在 function 外面取得 function 裡面的變數？

做一個全域變數，用它的屬性把值帶出來

```js
var a = {}

function test(){
  var b = 10
  a.b = b
}

test()
console.log(a.b)
```

瀏覽器有 window 可以用
甚至 window 的屬性就是全域變數

```js
function test(){
  var b = 10
  window.b = b
}

test()
console.log(window.b)
console.log(b)
```


