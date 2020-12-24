# 12/01(二) JavaScript
###### tags: `JavaScript`

### 觀念
* Javascript習慣兩格空格做縮排分段
* 分號「；」在JavaScript就算不加上，也會經由Automatic Semicolon Insertion加入
* 若想在JavaScript上進行return的換行，而不會因為ASI而出現undefine的話，則加入小括號。
* ![](https://i.imgur.com/uGYzOJz.png)
* Var以function為範圍scope，let以block為範圍scope

### 函式
* 在找外部Scope作用範圍，依據詞彙找外部
```
// lexical scope
var x = 1;
function a() {
  console.log(x);
}

function b() {
  var x = 2;
  a();
}

b();
```

* function可以包function
```
//var x = 1;
function a() {
  //var x = 2;
  function b() {
    //var x = 3
    console.log(x)
  }
  b();
}

a();
```

* 只有b能夠複寫，a只能刪減少東西
```
const a = []
let b = []
b = [1, 2, 3]
```

### 單一執行緒 single thread
* 一次只能做一件事情
```
function bigFun() {
  for(var i = 0; i < 100000000; i ++) {}
}
console.log(1)
bigFun()
console.log(2)
```

* JS定義了setTimeout, fetch，並且丟給runtime來做
```
setTimeout(function() {
    console.log(3);
}, 2000);
```
* ![](https://i.imgur.com/zM5w1Th.png)
* Queue要不要回來，要先看stack上面有沒有東西，才能回來。所以上述的setTimeout最快兩秒才會回來
* https://www.youtube.com/watch?v=8aGhZQkoFbQ
* ![](https://i.imgur.com/WWn1QcR.png)

### 自動轉型規則
* https://thomas-yang.me/projects/oh-my-dear-js/

### 嚴格模式 use strict
* 使得沒有宣告的變數會無法run
* 可以寫在function裡面，或者在整份文件的第一行。
* 注意是字串!!  'use strict'，用字串的原因是萬一瀏覽器不支援的話，可以讓它顯示為一個字串而已。

```
function a(){
    'use strict'
    x = 2
    console.log(x)
}
```

### 陳述句statement vs 表達式expression
* 表達式expression通常有回傳值
* a = 1 expression
* var a startment
```

if (a==1){
    console.log("x")
} else{
    console.log("y")
}
```
### JS中function是物件
```
function a(){
    return 2;
}

console.log(a);  這個會印出function
console.log(a());  印出2
```

### higher order function
* 如果這個function可以接收一個或數個function作為輸入，則稱。
```
const twice = (f, v) => f(f(v));
const add3 = v => v + 3;

twice(add3, 7); // 13
```

### template literal
* console.log(`hi`) 樣板字面值
```
Var obj = {}   // literal
Var obj = Object.create(null)
obj.name = "aa"
obj.age = 18

console.log(obj);
```

### 英雄產生器方程式
```
const goku = heroCreator('悟空', 100)
console.log(goku)
goku.attack()

function heroCreator(name, power) {
  // return {
  //   name, 
  //   power, 
  //   attack: function() { 
  //     console.log(`${this.name} 造成 ${this.power} 點的傷害`);
  //   }
  // }

  const hero = {}
  hero.name = name
  hero.power = power
  hero.attack = function() { 
    console.log(`${this.name} 造成 ${this.power} 點的傷害`);
  }
  return hero;
}
```
### 面試題目
https://github.com/lydiahallie/javascript-questions/blob/master/zh-TW/README_zh-TW.md


### 下星期一教this