# 12/09(三)西瓜-透過 JavaScript 進行 HTTP 請求 & 非同步
###### tags: `JavaScript`

### 觀念
* `By ${posts[0].author}`

### HTTP request
* 通訊協定
* ![](https://i.imgur.com/LWzCntc.png)

#### Gmail可以在不換頁的情形下開啟信件，是透過JavaScript進行HTTP request達成的

### fetch
* https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API
* 近兩三年發展的
* 之前透過$.ajax() https://api.jquery.com/jquery.ajax/
* 以及透過 HMLHttpRequest https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest

### 06-fetch first post
```
fetch(...)
  .then(request => request.json())
  .then(posts => { ... })
```

#### Arrow function 胖箭頭的解釋=>
* 書上GBS.SA5-PA4
* Arrow function的兩大好處：語法簡潔、this變數強制綁定
* 無法使用argument物件

* 只有一個參數時，小括號()可以省略
```
const hello = meg => console.log(meg);
hello('hello'); 
```
* 沒有參數時，小括號()不能省略
```
const hello = () => console.log('hello');
hello(); 
```


```
var test = (a, b) => a + b
test(1, 2) = 3
```
        
```
(a, b) => {
  console.log(a, b)
  return a + b
}
```

```
function(response) {
  return response.json
}
##### 上下等同
response => response.json()
```

#### 呼叫函式的方法
* function()
* function.call(這邊是函式執行的this, 1, 2)
* function.apply(這邊是函式執行的this, [1, 2])
* 函式被呼叫時，會產生argument物件，其實就是所帶入的參數
* argument.callee指目前執行的方程式，可以執行遞迴，在匿名函式特別有效
* argument並非陣列，但可以透過slice, ES6的Array.from將其轉成一個新的陣列

#### 箭頭function不能使用arugment，怎麼辦?
* 當函式最後一個參數以「...」開頭，則會將全部參數存入一個陣列中


### Cross-origin resource sharing
* Response Headers裡面的Access-Control-Allow-Origin: *  ，允許他站存取跨站存取資料

### 同步
```
* 把牛奶放入微波爐();
等待微波完成(); // <- 無法回應別的顧客
微波完成，拿給消費者();
```

### 非同步
* 告訴他，當你完成某件事情時去做什麼事情

#### Callback function
* 當某個條件被觸發，才被動的去執行某件事

#### Promise
```
const promise = new Promise(function(resolve, reject) {
  // 成功時
  resolve(value);
  // 失敗時
  reject(reason);
});

promise.then(
  function(value) {
    // on fulfillment(已實現時)
  },
  function(reason) {
    // on rejection(已拒絕時)
  }
);
```
* fetch回傳promise
* 可以chain，例如：.then(callback).then(callback)
* 錯誤處理，.catch(callback)
* ![](https://i.imgur.com/A8j1JrN.png)

[從Promise開始的JavaScript異步生活書本](http://promise.eddychang.me/docs/contents/ch1_intro
* https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
* https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then


#### Promise的特性，async與awit
* 使用的方式很簡單，我們只需要在定義 function 時， 前面加個 async
* * async () => {}
* * async function() {}
* * async function name() {}
[從 JavaScript Promise 到 Async Await
](https://w3c.hexschool.com/blog/b6d5db8?fbclid=IwAR3iEkFrHDlEidnbgF6Tdy1nsrToRbXc3hnL4odM2b_G2wnuRtEE4PSEwJg)

#### 做驗證
* https://github.com/5xTraining/pastleo-js-posts-api/blob/master/app/controllers/posts_controller.rb#L105