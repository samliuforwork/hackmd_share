# 12/22(二)奶綠-React
###### tags: `JavaScript` `React`

### 觀念
* https://zh-hant.reactjs.org/docs/introducing-jsx.html
* 蝦皮採用前後端分離模式，畫面都以Javascript來render出來。(PCHOME用伺服器後端來render)
* 安裝TO tree、jsES6 snipe、live server
* 要同時載入react、react-dom(index.html裡面)
* ![](https://i.imgur.com/GK6AIkT.png)
* ![](https://i.imgur.com/q7LRQa6.png)
* 之所以載入babel，是為了讓JS轉譯成瀏覽器能懂的code，瀏覽器看不懂JSX(此次版本作為教學用)
* babel看到 <script type="text/babel" src="app.js"></script>，就會自動編譯所以效能較不好。
* 根據網頁業界開發的淺規則，版號解釋17.0.1 , (破壞性更動,增加新的功能函式、能夠相容舊版本,修正小bug)，潛規則是最後面單號通常不穩定。但是對於react來說，16升到17可以直接升！
* React不能全域控制，react只要專注在data binding
* 迴圈裡面的vitrual DOM要加key
* 重新render的條件，set函式更新與props更新
* useRef用來操作洞元素

#### JSX是什麼？
https://www.geeksforgeeks.org/reactjs-introduction-jsx/?ref=rp
* 在js裡面寫類似HTML的語法，長得很像HTML但是不是。
* div裡面的class要取叫做「className」！
* 只要JSX裡面用大括號包起來的，都會進行JS運算
* Why JSX?
```
It is faster than normal JavaScript as it performs optimizations while translating to regular JavaScript.
It makes easier for us to create templates.
Instead of separating the markup and logic in separated files, React uses components for this purpose. We will learn about components in details in further articles.
```

#### ReactDom.reder()
* vitual DOm意旨原生不在網頁的元素
* 型別順序：JSX元素(很像HTML的元素!)、JS code塞動元素
```
* ReactDOM.render(
  <h1>Hello, World</h1>,
  document.getElementById('app')
)
```

#### component
* React裡面都是滿滿的component，再把想要重複的用迴圈跑出來
* props是從外部傳進來的，state是自己內部的變數
* props的關鍵字只有「children」

###### React.useEffect()
* 生命週期：component被建立的時候、component死亡的時候，建立與死亡都只會發生一次，通常會在零件被建立時產生一API，初始化什麼可以掛在被建立的時候，死亡時也可以卸載東西。
```
*   React.useEffect(() => {
    console.log('componentDidMount')
    // 建立時印出上面這段
    return () => {
      console.log('componentWillUnmount');
      // 死亡時return印出上面這段
    }
  }, []);
```
* https://www.mdeditor.tw/pl/pKa9/zh-tw

#### useState
* 所有變數異動都要透過setCount
```
* var [count, setCount] = React.useState(props.count);
  var arr = React.useState(props.count)
  var count = arr[0]
  var setCount = arr[1]
```
