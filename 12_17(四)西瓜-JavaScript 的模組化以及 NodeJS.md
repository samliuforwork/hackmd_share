# 12/17(四)西瓜-JavaScript 的模組化以及 NodeJS
###### tags: `JavaScript`

### 觀念
* 瀏覽器並沒有require這個方法，是源自於NodeJS的
* ECMAScript (or ES)是一套訂定標準，ES module給予了import / export關鍵字
* 所有的type='module'都是嚴格模式
* echo $? 回傳前一個程式碼回傳值
* npm install --save fast-csv(--save幫我寫入package.json)
* npx執行下去會先看我的node_modules/.bin底下有沒有webpack，若沒有則上網抓取
* nodejs只看得懂require，而webpack會把import轉換為require。

![](https://i.imgur.com/grGLhzv.png)
1. for main.js
```
import addOne from './addOne.js'
import { timeoutPromise, removeGreeting } from './utils.js'
```
2. for addOne.js
```
import { timeoutPromise } from './utils.js'
export default addOne;
```
3. for Utils.js
```
export const timeoutPromise = ms => new Promise((resolve, _reject) => {
  setTimeout(() => {
    resolve();
  }, ms);
})

export const removeGreeting = () => {
  const greetingDiv = document.getElementById('greeting');
    if (greetingDiv) {
      greetingDiv.remove();
    }
}
```
### JSON.stringify(value[, replacer[, space]])
* 可以將JS的物件或數值轉換成JSON格式，
* value:The value to convert to a JSON string.
* replacer Optional:
* https://www.mdeditor.tw/pl/pyDg/zh-tw

### process.avrg
* process.argv，這是一個陣列（Array 實例），索引 0 是 'node' 指令名稱，索引 1 是你的 .js 檔案路徑，如果有指定引數的話，這些引數會是從索引 2 開始儲存。
* https://ithelp.ithome.com.tw/articles/10231218

#### Array(3).fill()

