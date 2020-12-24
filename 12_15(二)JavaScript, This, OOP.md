# 12/15(二)JavaScript, This, OOP
###### tags: `龍哥`

### 課堂例題1
```
for(var i = 0; i < 5; i++) {
}
console.log(i); 
執行結果會是5，因為var作用範圍scope是function，因此不會被影響到，但如果是let就會了
```

### 課堂例題2
![](https://i.imgur.com/8lyGsj4.png)

### 物件導向
```
function heroCreator(name, action) {
const h= { name, action}
}

function heroCreator(name, action) {
const h= { name:name, action:action}
}
```
#### 解構式寫法
```
let name = goku.name
let action = goku.action
等同於
let { name, action } = goku
```

http://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html

### a.__proto__的效能比較差
* 所以使用Object.getPrototypeOf(a)

### new xxx

### 所有的function都有prototype的屬性
* 指向一個空陣列

function hero() {
 this.name = name
 this.age = age
}

const h1 = hero()
1.泡泡
2.return 123

const h2 = new hero()
1.泡泡
2.建立空物件{}
3.做出this指向空物件{}
4.把{}.__proto__ -> function.prototype
5.return this

![](https://i.imgur.com/gNO7ZFk.png)
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new

## This
* depend on runtime
* 在瀏覽器的this-window, node的this-global
### This規則
* 規則 1. 函數執行的時候，有沒有使用 `new` 關鍵字？如果有，`this` 就是指向那個物件本身。
* 規則 2. 「誰呼叫，誰就是 `this`」規則。跟this寫在哪無關，前面沒有小數點，就是global
* 規則 3. 是否使用箭頭函數？有的話就不會有自己的 `this`。
* 規則 4. 是否有使用 `bind`、`apply` 或是 `call` 方法？有的話 `this` 的指向也會跟著改變。
* 規則 5. 是否有開啟「嚴格模式」？
```
function hello() {
  console.log(this);  // 會印出什麼？

  function world() {
    console.log(this);  // 會印出什麼？

    const game = {
      name: "Zelda",
      greeting: function() {
        console.log(this); // 會印出什麼？
      }
    }
    game.greeting();
  }

  world();
}

hello();
```

#### bind
綁架h -> this
consy hAttack = attack.bind(h) //回傳一個新function

#### apply
* 直接呼叫h且當作this用

#### call
* 與apply差別在於參數數量不同

```
var hero = {
  name: '悟空',
  sayMyName: function() {
    console.log(this.name);
  }
};

hero.sayMyName();   // A

var speakOut = hero.sayMyName;
speakOut();         // B

const someone = { name: '路人' }

hero.sayMyName.call(someone);  // C

function here() {
  console.log(this);
}

const there = () => {
  console.log(this);
}

here();   // D
there();  // E
```

###### A 悟空 B undefined C 路人 D global E global